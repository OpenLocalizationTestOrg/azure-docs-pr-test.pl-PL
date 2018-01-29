---
title: "Rozwiązywanie problemów z kopii zapasowej błędy maszyny wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z kopii zapasowej i przywracania maszyn wirtualnych platformy Azure"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 73214212-57a4-4b57-a2e2-eaf9d7fde67f
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/21/2018
ms.author: trinadhk;markgal;jpallavi;
ms.openlocfilehash: d8840d2561e6102fe1679c36e981de6614b84d54
ms.sourcegitcommit: 1fbaa2ccda2fb826c74755d42a31835d9d30e05f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/22/2018
---
# <a name="troubleshoot-azure-virtual-machine-backup"></a>Rozwiązywanie problemów z kopiami zapasowymi maszyn wirtualnych platformy Azure
Można rozwiązać błędów napotkanych podczas przy użyciu usługi Kopia zapasowa Azure informacje wymienione w poniższej tabeli.

## <a name="backup"></a>Backup

### <a name="error-the-specified-disk-configuration-is-not-supported"></a>Błąd: Określona konfiguracja dysku nie jest obsługiwana

> [!NOTE]
> Mamy prywatnej wersji zapoznawczej do obsługi kopii zapasowych dla maszyn wirtualnych o > dysków 1TB. Aby uzyskać szczegółowe informacje, zobacz [prywatnej wersji zapoznawczej do obsługi kopii zapasowych dużych dysków maszyny Wirtualnej](https://gallery.technet.microsoft.com/Instant-recovery-point-and-25fe398a)
>
>

Kopia zapasowa Azure nie obsługuje obecnie rozmiary dysków [większa niż 1023GB](https://docs.microsoft.com/azure/backup/backup-azure-arm-vms-prepare#limitations-when-backing-up-and-restoring-a-vm). 
- Jeśli masz dyski większe od 1 TB, [dołącz nowe dyski](https://docs.microsoft.com/azure/virtual-machines/windows/attach-managed-disk-portal) o rozmiarze poniżej 1 TB. <br>
- Następnie skopiuj dane z dysku większego od 1 TB na nowo utworzone dyski mniejsze niż 1 TB. <br>
- Upewnij się, że wszystkie dane zostały skopiowane, a następnie usuń dyski większe od 1 TB.
- Zainicjuj tworzenie kopii zapasowej.

| Szczegóły błędu | Obejście problemu |
| --- | --- |
| Nie można wykonać operacji, ponieważ maszyna wirtualna już nie istnieje. -Zatrzymaj ochronę maszyny wirtualnej bez usuwania danych kopii zapasowej. Więcej szczegółów na http://go.microsoft.com/fwlink/?LinkId=808124 |Dzieje się tak w przypadku podstawowej maszyny Wirtualnej zostanie usunięty, ale zasady tworzenia kopii zapasowych nadal wyszukiwania dla maszyny Wirtualnej utworzyć kopię zapasową. Aby naprawić ten błąd: <ol><li> Utwórz ponownie maszynę wirtualną o tej samej nazwie i tej samej nazwy grupy zasobów [nazwa usługi w chmurze],<br>(OR)</li><li> Zatrzymaj ochronę maszyny wirtualnej z lub bez usuwania danych kopii zapasowej. [Więcej informacji](http://go.microsoft.com/fwlink/?LinkId=808124)</li></ol> |
| Operacja migawki nie powiodło się ze względu na brak łączności sieciowej na maszynie wirtualnej - upewnij się, że maszyna wirtualna ma dostęp do sieci. Dla migawki zakończyła się powodzeniem albo listę dozwolonych adresów IP centrum danych Azure zakresów lub ustawienie serwera proxy dla dostępu do sieci. Więcej informacji można znaleźć w http://go.microsoft.com/fwlink/?LinkId=800034. Jeśli korzystasz już z serwera proxy, upewnij się, że ustawienia serwera proxy są skonfigurowane prawidłowo | Ten błąd jest zgłaszany w przypadku zablokowania wychodzące połączenie z Internetem na maszynie wirtualnej. Połączenie z Internetem jest wymagany dla rozszerzenia migawki maszyny Wirtualnej z migawki odpowiednie dyski maszyny wirtualnej. [Dowiedz się więcej](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#snapshot-operation-failed-due-to-no-network-connectivity-on-the-virtual-machine) naprawy migawki błędy z powodu dostępu do sieci zablokowane. |
| Agent maszyny Wirtualnej nie może nawiązać połączenia z usługą kopia zapasowa Azure. -Upewnij się, czy maszyna wirtualna ma łączność sieciową i agenta maszyny Wirtualnej jest najnowsze i uruchomiona. Aby uzyskać więcej informacji zapoznaj się http://go.microsoft.com/fwlink/?LinkId=800034 |Ten błąd jest zgłaszany, jeśli występuje problem z agentem maszyny Wirtualnej lub dostępu do sieci do infrastruktury platformy Azure są zablokowane w inny sposób. [Dowiedz się więcej](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#vm-agent-unable-to-communicate-with-azure-backup) informacje o debugowaniu zapasowej maszyny Wirtualnej migawki problemy.<br> Jeśli agent maszyny Wirtualnej nie powoduje żadnych problemów, a następnie uruchom ponownie maszynę Wirtualną. W czasie niepoprawny stan maszyny Wirtualnej mogą powodować problemy, i ponownego uruchamiania maszyny Wirtualnej resetuje to "nieprawidłowego stanu". |
| Maszyna wirtualna jest w stanie niepowodzenia inicjowania obsługi administracyjnej — Uruchom ponownie maszynę Wirtualną i upewnij się, że maszyna wirtualna jest w stanie uruchomienia lub zamknięcia do utworzenia kopii zapasowej | Dzieje się tak, gdy jeden z błędami rozszerzenia prowadzi stan maszyny Wirtualnej w stanie niepowodzenia inicjowania obsługi administracyjnej. Przejdź do listy rozszerzeń i czy ma rozszerzenia nie powiodło się, usuń go i spróbuj ponownie uruchomić maszynę wirtualną. Jeśli wszystkie rozszerzenia są w stanie uruchomienia, sprawdź, czy Usługa agenta maszyny Wirtualnej jest uruchomiona. Jeśli nie, uruchom ponownie usługę agenta maszyny Wirtualnej. | 
| VMSnapshot rozszerzenia operacja nie powiodła się dla zarządzanych dysków, ponów operację tworzenia kopii zapasowej. Jeśli problem się powtarza, postępuj zgodnie z instrukcjami w "http://go.microsoft.com/fwlink/?LinkId=800034". Jeśli problem będzie dalej, skontaktuj się z pomocą techniczną firmy Microsoft | Ten błąd w przypadku niepowodzenia wyzwolenia migawki usługi Kopia zapasowa Azure. [Dowiedz się więcej](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#vmsnapshot-extension-operation-failed) informacje o debugowaniu wirtualna migawki problemy. |
| Można kopiowania migawki maszyny wirtualnej z powodu wolnego miejsca na koncie magazynu - Sprawdź, czy konto magazynu ma wolnego miejsca odpowiednikiem danych na dyskach magazynu premium dołączony do maszyny wirtualnej | W przypadku maszyn wirtualnych w warstwie premium możemy skopiować migawki do konta magazynu. To, aby upewnić się, że ruch związany z zarządzaniem kopii zapasowej, który działa na migawki, nie ograniczają liczbę IOPS dostępne do aplikacji przy użyciu dysków premium. Firma Microsoft zaleca się, że przydzielone tylko 50% całkowitego konta miejsca do magazynowania, usługi Azure Backup można skopiować migawki do przechowywania konta i transfer danych z tej lokalizacji skopiowany na koncie magazynu do magazynu. | 
| Nie można wykonać operacji, ponieważ agent maszyny Wirtualnej nie jest elastyczny |Ten błąd jest zgłaszany, jeśli występuje problem z agentem maszyny Wirtualnej lub dostępu do sieci do infrastruktury platformy Azure są zablokowane w inny sposób. Dla maszyn wirtualnych systemu Windows Sprawdź stan usługi agenta maszyny Wirtualnej w usługach i czy agent jest wyświetlane w aplecie Programy w Panelu sterowania. Spróbuj usunąć program z kontrolki panelu i ponowne zainstalowanie agenta, jak wspomniano [poniżej](#vm-agent). Po ponownym zainstalowaniu agenta, Wyzwól kopię zapasową adhoc można zweryfikować. |
| Operacja rozszerzenia usług odzyskiwania nie powiodła się. -Należy upewnić się, że najnowsza wersja agenta maszyny wirtualnej jest zainstalowany na maszynie wirtualnej i jest uruchomiona usługa agenta. Ponów operację tworzenia kopii zapasowej i w przypadku niepowodzenia skontaktuj się z pomocą techniczną firmy Microsoft. |Ten błąd jest zgłaszany, gdy agent maszyny Wirtualnej jest nieaktualny. Zobacz sekcję "Aktualizacja agenta maszyny Wirtualnej" poniżej, aby zaktualizować agenta maszyny Wirtualnej. |
| Maszyna wirtualna nie istnieje. -Podaj upewnij się, że istnieje maszyny wirtualnej, lub wybierz inną maszynę wirtualną. |Dzieje się tak, gdy podstawowej maszyny Wirtualnej jest usuwane, ale zasady tworzenia kopii zapasowych w dalszym ciągu wyszukiwania dla maszyny Wirtualnej wykonać kopię zapasową. Aby naprawić ten błąd: <ol><li> Utwórz ponownie maszynę wirtualną o tej samej nazwie i tej samej nazwy grupy zasobów [nazwa usługi w chmurze],<br>(OR)<br></li><li>Zatrzymaj ochronę maszyny wirtualnej bez usuwania danych kopii zapasowej. [Więcej informacji](http://go.microsoft.com/fwlink/?LinkId=808124)</li></ol> |
| Wykonanie polecenia nie powiodło się. -Inna operacja jest obecnie w toku dla tego elementu. Czekaj, aż do zakończenia poprzedniej operacji, a następnie spróbuj ponownie |Istniejącej kopii zapasowej na maszynie Wirtualnej jest uruchomiona, i nie można rozpocząć nowego zadania, istniejące zadanie jest uruchomiona. |
| Kopiowanie wirtualnych dysków twardych z magazynu kopii zapasowych został przekroczony — spróbuj ponownie wykonać operację w ciągu kilku minut. Jeśli problem będzie nadal występować, skontaktuj się z pomocą techniczną firmy Microsoft. | Dzieje się tak, jeśli jest to przejściowy błąd po stronie magazynu lub usługi tworzenia kopii zapasowej będzie niedługo wystarczające IOPS z konta magazynu obsługującego maszyny Wirtualnej w celu transferu danych przed upływem limitu czasu do magazynu. Upewnij się, że zostały wykonane [najlepsze rozwiązania](backup-azure-vms-introduction.md#best-practices) podczas konfigurowania kopii zapasowej. Spróbuj przenieść maszyny Wirtualnej do innego magazynu konta który nie został załadowany i ponów próbę wykonania kopii zapasowej.|
| Kopii zapasowej nie powiodło się z powodu wewnętrznego błędu - spróbuj ponownie wykonać operację w ciągu kilku minut. Jeśli problem będzie się powtarzać, skontaktuj się z pomocą techniczną firmy Microsoft Support |Ten błąd 2 powodów: <ol><li> Podczas uzyskiwania dostępu do magazynu maszyny Wirtualnej jest to problem przejściowy. Sprawdź, czy [stan Azure](https://azure.microsoft.com/en-us/status/) się czy ma żadnych problem związany z obliczeniowe w toku, pamięci masowej lub sieci w regionie. Po usunięciu problemu spróbuj zadanie tworzenia kopii zapasowej. <li>Oryginalna maszyna wirtualna została usunięta i dlatego nie można pobrać punktu odzyskiwania. Aby przechowywać dane kopii zapasowej dla usuniętych maszyny Wirtualnej, ale Usuń błędy tworzenia kopii zapasowej: Wyłącz ochronę maszyny Wirtualnej, a następnie wybierz opcję, aby zachować te dane. Ta akcja spowoduje zatrzymanie zaplanowane zadanie tworzenia kopii zapasowej i cyklicznego komunikaty o błędach. |
| Nie można zainstalować rozszerzenia usług odzyskiwania Azure na wybrany element — agent maszyny Wirtualnej jest wymaganiem wstępnym dla rozszerzenia usług odzyskiwania Azure. Zainstaluj agenta maszyny Wirtualnej platformy Azure i ponownie uruchom operację rejestracji |<ol> <li>Sprawdź, czy agent maszyny Wirtualnej został poprawnie zainstalowany. <li>Upewnij się, że została poprawnie ustawiona flaga w konfiguracji maszyny Wirtualnej.</ol> [Dowiedz się więcej](#validating-vm-agent-installation) o instalowaniu agenta maszyny Wirtualnej oraz sposób weryfikowania instalacji agenta maszyny Wirtualnej. |
| Instalacja rozszerzenia nie powiodło się z powodu błędu "COM + nie może komunikować się Microsoft Distributed Transaction Coordinator |Zwykle oznacza to, że usługa modelu COM + nie jest uruchomiona. Aby uzyskać pomoc dotyczącą rozwiązywania tego problemu, skontaktuj się z pomocą techniczną firmy Microsoft. |
| Migawki operacja nie powiodła się z powodu błędu operacji VSS "ten dysk jest zablokowany przez szyfrowanie dysków funkcją BitLocker. Należy odblokować ten dysk z poziomu Panelu sterowania. |Wyłącz funkcję BitLocker dla wszystkich dysków na maszynie Wirtualnej i sprawdź, czy usługi VSS problem został rozwiązany |
| Maszyna wirtualna nie jest w stanie, który umożliwia tworzenie kopii zapasowych. |<ul><li>Sprawdź, czy maszyna wirtualna jest w stan przejściowy między uruchamiania i wyłączanie w dół. Jeśli tak jest, poczekaj, aż stan maszyny Wirtualnej, jeden z nich i wyzwolić kopię zapasową ponownie. <li> Jeśli maszyna wirtualna jest maszyny Wirtualnej systemu Linux i używa [Linux zwiększonych zabezpieczeń] jądra modułu, należy wyłączyć ścieżki agenta systemu Linux (_/var/lib/waagent_) z zabezpieczeń są instalowane zasad, aby upewnić się, że zapasowy numer wewnętrzny.  |
| Nie można odnaleźć maszyny wirtualnej platformy Azure. |Dzieje się tak, gdy podstawowej maszyny Wirtualnej jest usuwane, ale zasady tworzenia kopii zapasowych w dalszym ciągu wyszukiwania dla maszyny Wirtualnej wykonać kopię zapasową. Aby naprawić ten błąd: <ol><li>Utwórz ponownie maszynę wirtualną o tej samej nazwie i tej samej nazwy grupy zasobów [nazwa usługi w chmurze], <br>(OR) <li> Wyłącz ochronę dla tej maszyny Wirtualnej, dlatego zadania tworzenia kopii zapasowej nie zostanie utworzona. </ol> |
| Agent maszyny wirtualnej nie znajduje się na maszynie wirtualnej — należy zainstalować wszystkie wymagania wstępne i agenta maszyny Wirtualnej, a następnie ponownie uruchom operację. |[Dowiedz się więcej](#vm-agent) informacji o instalacji agenta maszyny Wirtualnej i sprawdzania poprawności instalacji agenta maszyny Wirtualnej. |
| Operacja migawki nie powiodła się z powodu składniki zapisywania usługi VSS w złym stanie |Musisz ponownie uruchomić zapisywania usługi VSS (usługi kopiowania woluminów w tle), które znajdują się w złym stanie. Aby to osiągnąć, w wierszu polecenia z podwyższonym poziomem uprawnień, uruchom _vssadmin listy autorów_. Dane wyjściowe zawierają wszystkie składniki zapisywania usługi VSS i ich stan. Dla każdego składnika zapisywania usługi VSS nie "[1] stabilny" ma stan Uruchom ponownie składnik zapisywania usługi VSS, uruchamiając następujące polecenia z wiersza polecenia z podwyższonym poziomem uprawnień:<br> _polecenie net stop serviceName_ <br> _polecenie net start serviceName_|
| Operacja migawki nie powiodła się z powodu błędu podczas analizowania konfiguracji |Dzieje się z powodu zmiany uprawnień do katalogu MachineKeys: _%systemdrive%\programdata\microsoft\crypto\rsa\machinekeys_ <br>Uruchom poniżej polecenia i sprawdź, czy te domyślne uprawnienia do katalogu MachineKeys:<br>_icacls %systemdrive%\programdata\microsoft\crypto\rsa\machinekeys_ <br><br> Domyślne uprawnienia to:<br>Everyone:(R,W) <br>BUILTIN\Administrators:(F)<br><br>Jeśli widzisz uprawnienia w katalogu MachineKeys inne niż domyślne, wykonaj następujące czynności, aby poprawić uprawnienia, usunąć certyfikat i wyzwolić tworzenie kopii zapasowej.<ol><li>Napraw uprawnienia w katalogu MachineKeys.<br>Przy użyciu Eksploratora właściwości zabezpieczeń i zaawansowane ustawienia zabezpieczeń w katalogu, Zresetuj uprawnienia do wartości domyślnych, Usuń dowolnego obiektu użytkownika dodatkowe (niż ustawienie domyślne) z katalogu i upewnij się, że "Wszyscy" uprawnień miał dostępu specjalnego dla:<br>-Wyświetlanie zawartości folderu / Odczyt danych <br>— Przeczytaj atrybutów <br>-Atrybuty rozszerzone odczytu <br>-Tworzenie plików / Zapis danych <br>-Tworzenie folderów / Dołączanie danych<br>-Zapis atrybutów<br>-Atrybuty rozszerzone zapisu<br>-Uprawnienia do odczytu<br><br><li>Usuń wszystkie certyfikaty z polem "Wystawiony dla" = "Systemu Windows Azure usługi zarządzania dla rozszerzenia" lub "Systemu Windows Azure CRP certyfikatu generatora".<ul><li>[Otwórz konsolę Certyfikaty (komputer lokalny)](https://msdn.microsoft.com/library/ms788967(v=vs.110).aspx)<li>Usuń wszystkie certyfikaty (w obszarze osobiste -> certyfikatów) z polem "Wystawiony dla" = "Systemu Windows Azure usługi zarządzania dla rozszerzenia" lub "Systemu Windows Azure CRP certyfikatu generatora".</ul><li>Wyzwalacz kopii zapasowej maszyny Wirtualnej. </ol>|
| Sprawdzanie poprawności nie powiodła się, ponieważ maszyna wirtualna jest zaszyfrowana z BEK samodzielnie. Kopie zapasowe można włączyć tylko dla zaszyfrowanych za pomocą zarówno BEK i KEK maszyn wirtualnych. |Maszyna wirtualna powinna być szyfrowana przy użyciu zarówno klucz szyfrowania funkcją BitLocker, jak i klucz szyfrowania klucza. Po wykonaniu tej kopii zapasowej powinno być włączone. |
| Usługa Kopia zapasowa Azure nie ma wystarczających uprawnień do magazynu kluczy dla kopii zapasowej z zaszyfrowanych maszyn wirtualnych. |Usługa tworzenia kopii zapasowej należy podawać tych uprawnień w programie PowerShell przy użyciu czynności wymienionych w **włączenia kopii zapasowej** sekcji [dokumentacji programu PowerShell](backup-azure-vms-automation.md). |
|Instalacja migawki rozszerzenia nie powiodła się z powodu błędu — modelu COM + nie może komunikować się z koordynatorem transakcji rozproszonych firmy Microsoft | Spróbuj uruchomić usługi systemu windows "aplikacji COM + systemu" (z wiersza polecenia z podwyższonym poziomem uprawnień - _net start COMSysApp_). <br>W przypadku niepowodzenia podczas uruchamiania wykonaj następujące czynności:<ol><li> Sprawdź, czy konto logowania usługi "Distributed Transaction Coordinator" jest "Usługa sieciowa". Jeśli nie jest, zmień ją na 'Usługa sieciowa', ponownie uruchomić usługę, a następnie spróbuj uruchomić usługi "aplikacji COM + systemu". "<li>Jeśli nadal nie można uruchomić, odinstaluj/instalacji usługi "Distributed Transaction Coordinator" wykonując następujące czynności:<br> -Zatrzymać usługi MSDTC<br> -Otwórz okno wiersza polecenia (cmd) <br> — Uruchom polecenie "msdtc-odinstalować" <br> — Uruchom polecenie "msdtc-instalacji" <br> -Uruchomienie usługi MSDTC<li>Uruchom usługę systemu windows "aplikacji COM + systemu" i po jej uruchomieniu Wyzwól kopię zapasową z portalu.</ol> |
|  Operacja migawki nie powiodła się z powodu błędu modelu COM + | Zalecana akcja jest ponowne uruchomienie usługi systemu windows "aplikacji COM + systemu" (z wiersza polecenia z podwyższonym poziomem uprawnień - _net start COMSysApp_). Jeśli problem będzie nadal występował, uruchom ponownie maszynę Wirtualną. Jeśli ponowne uruchomienie maszyny Wirtualnej nie pomoże, spróbuj [Usuwanie rozszerzenia VMSnapshot](https://docs.microsoft.com/azure/backup/backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout#cause-3-the-backup-extension-fails-to-update-or-load) i ręcznie wyzwalanie tworzenia kopii zapasowej. |
| Nie można zablokować co najmniej jeden — punkty instalacji maszyny wirtualnej do tworzenia migawki spójne systemu plików | Wykonaj następujące czynności: <ol><li>Sprawdź stan wszystkich zainstalowanych urządzeń przy użyciu systemu plików _"tune2fs"_ polecenia.<br> Przykład: tune2fs -l/dev/sdb1 \| grep "Stan systemu plików" <li>Odinstaluj urządzeń, dla których filesystem stan nie jest czysty przy użyciu _"umount"_ polecenia <li> Uruchom sprawdzanie FileSystemConsistency na tych urządzeniach przy użyciu _"fsck"_ polecenia <li> Ponownie zainstaluj urządzenia, a następnie spróbuj kopii zapasowej.</ol> |
| Operacja migawki nie powiodła się z powodu błędu podczas tworzenia kanału komunikacyjnego bezpiecznej sieci | <ol><Li> Otwórz Edytor rejestru, uruchamiając regedit.exe w trybie podniesionych uprawnień. <li> Zidentyfikuj wszystkie wersje. NetFramework obecne w systemie. Znajduje się on w hierarchii klucza rejestru "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft" <li> Dla każdego z nich. NetFramework obecne w kluczu rejestru, Dodaj następujący klucz: <br> "SchUseStrongCrypto"=dword:00000001 </ol>|
| Operacja migawki nie powiodła się z powodu niepowodzenia instalacji pakietu redystrybucyjnego Visual C++ dla programu Visual Studio 2012 | Przejdź do C:\Packages\Plugins\Microsoft.Azure.RecoveryServices.VMSnapshot\agentVersion i zainstaluj vcredist2012_x64. Upewnij się, że wartości klucza rejestru dla ta instalacja usługi jest ustawiony na prawidłową wartość tj. wartość klucza rejestru _HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Msiserver_ ma ustawioną wartość 3 i 4 nie. Jeśli nadal są ukierunkowane problemy z instalacją, ponownie uruchom usługę instalacji przez uruchomienie _MSIEXEC/unregister_ następuje _MSIEXEC /REGISTER_ z wiersza polecenia o podniesionych uprawnieniach.  |


## <a name="jobs"></a>Zadania
| Szczegóły błędu | Obejście problemu |
| --- | --- |
| Anulowanie nie jest obsługiwana dla tego typu zadania — poczekaj, aż zadanie zostało ukończone. |Brak |
| Zadanie nie jest w stanie można anulować — poczekaj, aż zadanie zostało ukończone. <br>LUB<br> Wybrane zadanie nie jest w stanie można anulować — Zaczekaj na ukończenie zadania. |Najprawdopodobniej zadanie jest niemal ukończone. Poczekaj, aż do ukończenia zadania.|
| Nie można anulować zadania, ponieważ nie jest w toku — anulowania jest obsługiwana tylko dla zadania, które są w toku. Anuluj próba w toku zadania. |Dzieje się z powodu stanu przejściowymi. Poczekaj chwilę i ponów próbę wykonania operacji anulowania. |
| Nie można anulować zadania — proszę czekać dopóki zakończenie zadania. |Brak |

## <a name="restore"></a>Przywracanie
| Szczegóły błędu | Obejście problemu |
| --- | --- |
| Przywracanie nie powiodło się z powodu błędu wewnętrznego w chmurze |<ol><li>Usługi chmury, do której chcesz przywrócić jest skonfigurowany przy użyciu ustawień DNS. Możesz sprawdzić <br>$deployment = get-AzureDeployment - ServiceName "ServiceName"-miejsca "Production" Get-AzureDns - DnsSettings $deployment. DnsSettings<br>W przypadku skonfigurowany adres, oznacza to, czy ustawienia DNS są skonfigurowane.<br> <li>Usługi chmury, do której próbujesz przywrócić jest skonfigurowany z zastrzeżonego adresu IP i istniejących maszyn wirtualnych w usłudze w chmurze są w stanie zatrzymania.<br>Można sprawdzić, czy usługa w chmurze ma zastrzeżony adres IP za pomocą następujących poleceń cmdlet programu powershell:<br>$deployment = get-AzureDeployment - ServiceName "servicename"-gniazdo $ "Production" w programie dep. Nazwa zastrzeżonego adresu IP <br><li>Chcesz przywrócić maszynę wirtualną o następujące konfiguracje sieciowe specjalne w do tej samej usługi w chmurze. <br>— Maszyny wirtualne w konfiguracji usługi równoważenia obciążenia (wewnętrznych i zewnętrznych)<br>— Maszyny wirtualne z wielu zastrzeżonych adresów IP<br>— Maszyny wirtualne z wieloma kartami sieciowymi<br>Wybierz nową usługę w chmurze w interfejsie użytkownika lub zapoznaj się z [zagadnienia dotyczące przywracania](backup-azure-arm-restore-vms.md#restore-vms-with-special-network-configurations) dla maszyn wirtualnych z konfiguracjami sieci specjalnych.</ol> |
| Wybranej nazwy DNS jest już zajęta — Określ inną nazwę DNS i spróbuj ponownie. |Tutaj nazwę DNS, który odwołuje się do nazwy usługi w chmurze (zazwyczaj kończąc. cloudapp.net). To musi być unikatowa. Jeśli wystąpi ten błąd, należy wybrać inną nazwę maszyny Wirtualnej podczas przywracania. <br><br> Ten błąd jest wyświetlany tylko dla użytkowników portalu Azure. Operacji przywracania za pomocą programu PowerShell powiedzie się, ponieważ tylko przywraca dysków i nie tworzy maszynę Wirtualną. Błąd zostanie skierowany w przypadku maszyny Wirtualnej jest jawnie utworzone przez użytkownika, po operacji przywracania dysku. |
| Konfiguracja określonej sieci wirtualnej jest nieprawidłowa — Określ konfiguracji innej sieci wirtualnej i spróbuj ponownie. |Brak |
| Usługi w chmurze określonego używa zastrzeżonego adresu IP, który nie pasuje do konfiguracji maszyny wirtualnej przywracana — Określ innej usługi w chmurze, która nie używa zastrzeżonego adresu IP, lub wybierz inny punkt odzyskiwania, aby przywrócić z. |Brak |
| Usługi w chmurze osiągnięto limit liczby wejściowych punktów końcowych — spróbuj ponownie wykonać operację, określając innej usługi w chmurze lub przy użyciu istniejącego punktu końcowego. |Brak |
| Konto magazynu kopii zapasowej magazynu i obiekt docelowy znajdują się w dwóch różnych regionach — upewnij się, że wybrane konto magazynu podczas operacji przywracania jest w tym samym regionie Azure jako magazynu kopii zapasowych. |Brak |
| Konta magazynu określony dla operacji przywracania nie jest obsługiwana — konta magazynu tylko Basic/Standard z lokalnie nadmiarowego lub z magazynu geograficznie nadmiarowego replikacji ustawienia są obsługiwane. Wybierz konto magazynu obsługiwane |Brak |
| Typ konta magazynu określony dla operacji przywracania nie jest w trybie online — upewnij się, że konta magazynu określony w operacji przywracania jest w trybie online |Taka sytuacja może wystąpić z powodu błędu przejściowego w usłudze Azure Storage lub z powodu awarii. Wybierz inne konto magazynu. |
| Osiągnięto limit przydziału Grupa zasobów — Usuń niektóre grupy zasobów z portalu Azure lub skontaktuj się z pomocą techniczną platformy Azure w celu zwiększenia limitów. |Brak |
| Wybrana podsieć nie istnieje — Wybierz podsieć, która istnieje |Brak |
| Usługa Kopia zapasowa nie ma autoryzacji umożliwiającej dostęp do zasobów w Twojej subskrypcji. |Aby rozwiązać ten problem, pierwszy dysków przywracania przy użyciu czynności wymienionych w sekcji **przywracania kopii zapasowej dysków** w [Wybieranie konfiguracji maszyny Wirtualnej przywracania](backup-azure-arm-restore-vms.md#choose-a-vm-restore-configuration). Po tym, użyj programu PowerShell czynności wymienionych w [utworzyć Maszynę wirtualną z dysków przywróconej](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) Aby utworzyć pełny maszynę Wirtualną z przywróconą dysków. |

## <a name="backup-or-restore-taking-time"></a>Kopii zapasowej lub przywracania czasu
Jeśli widzisz Twojej backup(>12 hours) lub przywracania biorąc time(>6 hours):
* Zrozumienie [czynniki przyczyniające się do wykonywania kopii zapasowej](backup-azure-vms-introduction.md#total-vm-backup-time) i [czynniki przyczyniające się do przywrócenia czas](backup-azure-vms-introduction.md#total-restore-time).
* Upewnij się, że stosujesz [kopii zapasowej najlepsze rozwiązania w zakresie](backup-azure-vms-introduction.md#best-practices). 

## <a name="vm-agent"></a>Agent maszyny Wirtualnej
### <a name="setting-up-the-vm-agent"></a>Konfigurowanie agenta maszyny Wirtualnej
Zwykle agenta maszyny Wirtualnej jest już obecny na maszynach wirtualnych, które są tworzone z poziomu galerii Azure. Jednakże maszyn wirtualnych, które są migrowane z lokalnych centrów danych nie mieć zainstalowanego agenta maszyny Wirtualnej. Dla tych maszyn wirtualnych Agent maszyny Wirtualnej musi być jawnie zainstalowany.

Dla maszyn wirtualnych systemu Windows:

* Pobierz i zainstaluj [plik MSI agenta](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Do ukończenia procesu instalacji niezbędne są uprawnienia administratora.
* W przypadku maszyn wirtualnych Classic [Aktualizuj właściwości maszyny Wirtualnej](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) aby wskazać, że agent jest zainstalowany. Ten krok nie jest wymagane dla maszyn wirtualnych Menedżera zasobów.

Dla maszyn wirtualnych systemu Linux:

* Zainstaluj najnowsze z repozytorium dystrybucji. Firma Microsoft **zdecydowanie zaleca się** Instalowanie agenta tylko za pośrednictwem dystrybucji repozytorium. Aby uzyskać więcej informacji na nazwę pakietu, zapoznaj się [repozytorium agenta systemu Linux](https://github.com/Azure/WALinuxAgent) 
* Dla maszyn wirtualnych klasycznego [Aktualizuj właściwości maszyny Wirtualnej](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) aby wskazać, że agent jest zainstalowany. Ten krok nie jest wymagane dla maszyn wirtualnych Menedżera zasobów.

### <a name="updating-the-vm-agent"></a>Aktualizowanie agenta maszyny wirtualnej
Dla maszyn wirtualnych systemu Windows:

* Aktualizowanie agenta maszyny wirtualnej jest równie proste, jak ponowne zainstalowanie [plików binarnych agenta maszyny wirtualnej](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Jednak należy się upewnić, że żadna operacja tworzenia kopii zapasowej jest uruchomiony podczas aktualizacji agenta maszyny Wirtualnej.

Dla maszyn wirtualnych systemu Linux:

* Postępuj zgodnie z instrukcjami [aktualizacja agenta maszyny Wirtualnej systemu Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Firma Microsoft **zdecydowanie zaleca się** aktualizacji agenta tylko za pośrednictwem dystrybucji repozytorium. Nie zaleca się pobierania kodu agenta z bezpośrednio z witryny github i zaktualizowaniem go. Jeśli najnowsza wersja agenta nie jest dostępny do dystrybucji, sprawdź dotrzeć do dystrybucji pomocy technicznej, aby uzyskać instrukcje dotyczące sposobu instalowania najnowsza wersja agenta. Możesz sprawdzić najnowszych [agenta Windows Azure w systemie Linux](https://github.com/Azure/WALinuxAgent/releases) informacje zawarte w repozytorium github.

### <a name="validating-vm-agent-installation"></a>Sprawdzanie poprawności instalacji agenta maszyny Wirtualnej
Jak sprawdzić, czy wersja agenta maszyny Wirtualnej na maszynach wirtualnych systemu Windows:

1. Zaloguj się do maszyny wirtualnej platformy Azure i przejdź do folderu *C:\WindowsAzure\Packages*. Powinien znajdować się w nim plik WaAppAgent.exe.
2. Kliknij plik prawym przyciskiem myszy, przejdź do opcji **Właściwości**, a następnie wybierz kartę **Szczegóły**. Wersja produktu pole powinno być 2.6.1198.718 lub nowszej

## <a name="troubleshoot-vm-snapshot-issues"></a>Rozwiązywanie problemów migawki maszyny Wirtualnej
Zależy od wydawania polecenia migawki powiązany magazyn kopii zapasowej maszyny Wirtualnej. Nie ma dostępu do magazynu lub opóźnień w wykonywania zadania migawki może spowodować niepowodzenie zadania tworzenia kopii zapasowej. Następujące może spowodować niepowodzenie zadań migawki.

1. Dostęp sieciowy do przechowywania jest zablokowane, za pomocą grupy NSG<br>
    Dowiedz się więcej na temat [Włącz dostęp do sieci](backup-azure-arm-vms-prepare.md#establish-network-connectivity) magazynu przy użyciu albo listę dozwolonych podobnej adresów IP lub za pośrednictwem serwera proxy.
2. Maszyny wirtualne z skonfigurowano kopii zapasowej programu Sql Server może spowodować opóźnienie zadania migawki <br>
   Domyślnie maszyny Wirtualnej kopii zapasowych problemów VSS pełnej kopii zapasowej na maszynach wirtualnych systemu Windows. Na maszynach wirtualnych z systemami serwerów Sql i jeśli kopia zapasowa programu Sql Server jest skonfigurowany może to spowodować opóźnienia podczas wykonywania migawki. Ustaw następujący klucz rejestru, jeśli występują błędy kopii zapasowych z powodu problemów z migawki.

   ```
   [HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT]
   "USEVSSCOPYBACKUP"="TRUE"
   ```
3. Stan maszyny Wirtualnej zgłosić niepoprawnie, ponieważ maszyna wirtualna jest zamknięta w protokole RDP.  <br>
   Jeśli ma zamknąć maszyny wirtualnej w protokole RDP, sprawdź, czy w portalu czy stan maszyny Wirtualnej jest odzwierciedlana poprawnie. Jeśli nie, zamknij maszynę Wirtualną w portalu przy użyciu opcji "Zamknij", na pulpicie nawigacyjnym maszyny Wirtualnej.
4. Jeśli więcej niż cztery maszyny wirtualne korzystają z tej samej usługi w chmurze, można skonfigurować wiele zasad tworzenia kopii zapasowych, aby przemieścić kopii zapasowej razy więc nie ma więcej niż cztery kopii zapasowych maszyn wirtualnych są uruchamiane w tym samym czasie. Spróbuj rozkładu czasu od siebie między zasadami godzinę rozpoczęcia tworzenia kopii zapasowej.
5. Maszyna wirtualna jest uruchomiona na wysoki Procesora/pamięci.<br>
   Jeśli maszyna wirtualna jest uruchomiona na wysoki Procesora usage(>90%) lub pamięci, zadanie migawki jest w kolejce, opóźnienia i po pewnym czasie zostaną pobiera upłynął limit czasu. Spróbuj kopii zapasowej na żądanie w takich sytuacjach.

<br>

## <a name="networking"></a>Networking
Podobnie jak wszystkie rozszerzenia rozszerzenie usługi Backup wymagany dostęp do publicznego Internetu. Nie ma dostępu do publicznej sieci internet może sam manifestu na różne sposoby:

* Instalacja rozszerzenia może zakończyć się niepowodzeniem
* Operacje tworzenia kopii zapasowej (takie jak migawki dysku) może zakończyć się niepowodzeniem
* Wyświetlanie stanu operacji tworzenia kopii zapasowej może zakończyć się niepowodzeniem

Połączone przegubowo potrzebę rozpoznawania publiczne adresy internetowe [tutaj](http://blogs.msdn.com/b/mast/archive/2014/06/18/azure-vm-provisioning-stuck-on-quot-installing-extensions-on-virtual-machine-quot.aspx). Należy sprawdzić konfiguracje DNS dla sieci Wirtualnej i upewnij się, że identyfikator URI Azure mogą zostać rozwiązane.

Po rozpoznawanie nazw odbywa się prawidłowo, dostępu do adresów IP Azure również musi zostać zapewniony. Aby odblokować dostęp do infrastruktury platformy Azure, wykonaj jedną z następujących czynności:

1. Lista dozwolonych adresów centrum danych Azure zakresów adresów IP.
   * Pobierz listę [centrum danych Azure adresów IP](https://www.microsoft.com/download/details.aspx?id=41653) jako białej.
   * Odblokowywanie przy użyciu adresów IP [NetRoute nowy](https://technet.microsoft.com/library/hh826148.aspx) polecenia cmdlet. Uruchom to polecenie cmdlet w Maszynie wirtualnej Azure, w oknie programu PowerShell z podwyższonym poziomem uprawnień (Uruchom jako Administrator).
   * (Jeśli jest dostępny w miejscu), aby zezwolić na dostęp do adresów IP, należy dodać reguły do grupy NSG.
2. Tworzenie ścieżki dla przepływ ruchu HTTP
   * Jeśli masz niektóre ograniczenia sieci w miejscu (sieciową grupę zabezpieczeń, na przykład) wdrażanie serwera proxy HTTP do kierowania ruchem. Kroki wdrażania serwera HTTP Proxy można znaleźć [tutaj](backup-azure-arm-vms-prepare.md#establish-network-connectivity).
   * (Jeśli jest dostępny w miejscu) umożliwiają dostęp do INTERNETU z serwera HTTP Proxy, należy dodać reguły do grupy NSG.

> [!NOTE]
> DHCP musi być włączona na gościu IaaS kopii zapasowej maszyny Wirtualnej do pracy.  Jeśli potrzebujesz statycznego prywatnego adresu IP, należy skonfigurować go za pośrednictwem platformy. Opcja DHCP w ramach maszyny Wirtualnej powinna być włączona w lewo.
> Wyświetl więcej informacji o [ustawienie wewnętrzny statycznego prywatnego adresu IP](../virtual-network/virtual-networks-reserved-private-ip.md).
>
>
