---
title: "Agent usługi Azure Backup — często zadawane pytania | Microsoft Docs"
description: "Odpowiedzi na często zadawane pytania dotyczące sposobu działania agenta usługi Azure Backup oraz limitów wykonywania kopii zapasowych i przechowywania."
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
ms.openlocfilehash: 227cdc87f3e2c8ed393145f4bbde7f74606bdf3b
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="questions-about-the-azure-backup-agent"></a>Pytania dotyczące agenta usługi Azure Backup
W tym artykule znajdują się odpowiedzi na często zadawane pytania pomagające w szybkim poznaniu składników agenta usługi Azure Backup. W niektórych odpowiedziach znajdują się linki do artykułów zawierających szczegółowe informacje. Pytania dotyczące usługi Azure Backup można również zadawać na [forum dyskusyjnym](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="configure-backup"></a>Konfigurowanie kopii zapasowych
### <a name="where-can-i-download-the-latest-azure-backup-agent-br"></a>Gdzie można pobrać najnowszą wersję agenta usługi Azure Backup? <br/>
Najnowszą wersję agenta tworzenia kopii zapasowej systemu Windows Server, System Center DPM lub klienta systemu Windows można pobrać [tutaj](http://aka.ms/azurebackup_agent). Aby utworzyć kopię zapasową maszyny wirtualnej, należy skorzystać z agenta maszyny wirtualnej (który automatycznie instaluje właściwe rozszerzenie). Agent maszyny wirtualnej znajduje się już na maszynie wirtualnej, która została utworzona z poziomu galerii Azure.

### <a name="when-configuring-the-azure-backup-agent-i-am-prompted-to-enter-the-vault-credentials-do-vault-credentials-expire"></a>Podczas konfigurowania agenta usługi Azure Backup pojawia się monit o wprowadzenie poświadczeń magazynu. Czy poświadczenia magazynu wygasają?
Tak, poświadczenia magazynu wygasają po upływie 48 godzin. Jeśli plik wygaśnie, należy zalogować się do witryny Azure Portal i pobrać z magazynu pliki poświadczeń magazynu.

### <a name="what-types-of-drives-can-i-back-up-files-and-folders-from-br"></a>Z jakich typów dysków można tworzyć kopie zapasowe plików i folderów? <br/>
Nie można utworzyć kopii zapasowych następujących dysków/woluminów:

* Nośniki wymienne: wszystkie źródła elementów kopii zapasowych muszą być stałe.
* Woluminy tylko do odczytu: wolumin musi mieć możliwość zapisu ze względu na działanie usługi kopiowania woluminów w tle (VSS, volume shadow copy).
* Woluminy offline: wolumin musi być w trybie online, aby mogła działać usługa VSS.
* Udział sieciowy: wolumin musi być lokalny dla serwera, aby możliwe było wykonanie kopii zapasowej za pomocą usługi kopii zapasowej online.
* Woluminy chronione przez funkcję BitLocker: wolumin musi zostać odblokowany przed próbą wykonania kopii zapasowej.
* Identyfikacja systemu plików: jedyny obsługiwany system plików to system NTFS.

### <a name="what-file-and-folder-types-can-i-back-up-from-my-serverbr"></a>Jakie typy plików i folderów z serwera można umieszczać w kopiach zapasowych?<br/>
Obsługiwane są następujące typy:

* Zaszyfrowane
* Skompresowane
* Rozrzedzone
* Skompresowane i rozrzedzone
* Twarde linki: nieobsługiwane, pomijane
* Punkt ponownej analizy: nieobsługiwane, pomijane
* Zaszyfrowane i rozrzedzone: nieobsługiwane, pomijane
* Skompresowany strumień: nieobsługiwane, pomijane
* Rozrzedzony strumień: nieobsługiwane, pomijane

### <a name="can-i-install-the-azure-backup-agent-on-an-azure-vm-already-backed-by-the-azure-backup-service-using-the-vm-extension-br"></a>Czy można zainstalować agenta usługi Azure Backup na maszynie wirtualnej, której kopia zapasowa została już utworzona przez usługę Azure Backup przy użyciu rozszerzenia maszyny wirtualnej? <br/>
Naturalnie. Usługa Azure Backup udostępnia funkcję tworzenia kopii zapasowych na poziomie maszyny wirtualnej dla maszyn wirtualnych platformy Azure przy użyciu rozszerzenia maszyny wirtualnej. Aby chronić pliki i foldery znajdujące się w systemie operacyjnym Windows gościa, zainstaluj w tym systemie agenta usługi Azure Backup.

### <a name="can-i-install-the-azure-backup-agent-on-an-azure-vm-to-back-up-files-and-folders-present-on-temporary-storage-provided-by-the-azure-vm-br"></a>Czy można zainstalować agenta usługi Azure Backup na maszynie wirtualnej Azure, aby wykonywać kopie zapasowe plików i folderów znajdujących się w magazynie tymczasowym dostarczanym przez maszynę wirtualną platformy Azure? <br/>
Tak. Zainstaluj agenta usługi Azure Backup w systemie operacyjnym Windows gościa i wykonuj kopie zapasowe plików i folderów do magazynu tymczasowego. Zadania tworzenia kopii zapasowych zakończą się niepowodzeniem, gdy dane magazynu tymczasowego zostaną wyczyszczone. Ponadto usunięcie danych magazynu tymczasowego powoduje, że można je przywracać tylko do trwałego magazynu.

### <a name="whats-the-minimum-size-requirement-for-the-cache-folder-br"></a>Jaki jest minimalny wymagany rozmiar folderu pamięci podręcznej? <br/>
Rozmiar folderu pamięci podręcznej określa ilość danych, które można umieścić w kopii zapasowej. Folder pamięci podręcznej powinien udostępniać 5% miejsca wymaganego do przechowywania danych.

### <a name="how-do-i-register-my-server-to-another-datacenterbr"></a>Jak można zarejestrować serwer w innym centrum danych?<br/>
Dane kopii zapasowej są wysyłane do centrum danych magazynu, w którym jest ona zarejestrowana. Najprostszym sposobem zmiany centrum danych jest odinstalowanie agenta oraz ponowne zainstalowanie i zarejestrowanie go w nowym magazynie należącym do odpowiedniego centrum danych.

### <a name="does-the-azure-backup-agent-work-on-a-server-that-uses-windows-server-2012-deduplication-br"></a>Czy agent usługi Azure Backup działa na serwerze, który korzysta z deduplikacji systemu Windows Server 2012? <br/>
Tak. Podczas przygotowywania do wykonania kopii zapasowej usługa agenta konwertuje deduplikowane dane do zwykłej postaci. Następnie optymalizuje dane pod kątem utworzenia kopii zapasowej, szyfruje je, po czym wysyła zaszyfrowane dane do usługi kopii zapasowej online.

## <a name="backup"></a>Tworzenie kopii zapasowych
### <a name="how-do-i-change-the-cache-location-specified-for-the-azure-backup-agentbr"></a>W jaki sposób można zmienić lokalizację pamięci podręcznej określoną dla agenta usługi Azure Backup?<br/>
Użyj następującej listy, aby zmienić lokalizację pamięci podręcznej.

1. Należy zatrzymać aparat kopii zapasowej za pomocą następującego polecenia w wierszu polecenia z podwyższonym poziomem uprawnień:

    ```PS C:\> Net stop obengine``` 
  
2. Nie należy przenosić plików. Zamiast tego należy skopiować folder z obszarem pamięci podręcznej na inny dysk z wystarczającą ilością miejsca. Pierwotny obszar pamięci podręcznej można usunąć po potwierdzeniu, że kopie zapasowe działają z nowym obszarem pamięci podręcznej.
3. Należy zaktualizować następujące wpisy rejestru ścieżką do nowego folderu obszaru pamięci podręcznej.<br/>

    | Ścieżka rejestru | Klucz rejestru | Wartość |
    | --- | --- | --- |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config` |ScratchLocation |*Nowa lokalizacja folderu pamięci podręcznej* |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider` |ScratchLocation |*Nowa lokalizacja folderu pamięci podręcznej* |

4. Należy ponownie uruchomić aparat usługi Backup, wykonując następujące polecenie w wierszu polecenia z podwyższonym poziomem uprawnień:

    ```PS C:\> Net start obengine```

Po pomyślnym zakończeniu tworzenia kopii zapasowej w nowej lokalizacji pamięci podręcznej można usunąć pierwotny folder pamięci podręcznej.


### <a name="where-can-i-put-the-cache-folder-for-the-azure-backup-agent-to-work-as-expectedbr"></a>Gdzie można umieścić folder pamięci podręcznej, aby agent usługi Azure Backup działał zgodnie z oczekiwaniami?<br/>
Nie zaleca się używać następujących lokalizacji dla folderu pamięci podręcznej:

* Udział sieciowy lub nośniki wymienne: folder pamięci podręcznej musi być lokalny dla serwera, który wymaga wykonywania kopii zapasowych przy użyciu usługi kopii zapasowej online. Lokalizacje sieciowe ani nośniki wymienne, takie jak dyski USB, nie są obsługiwane.
* Woluminy offline: folder pamięci podręcznej musi być w trybie online dla oczekiwanej kopii zapasowej wykonywanej za pomocą agenta usługi Azure Backup.

### <a name="are-there-any-attributes-of-the-cache-folder-that-are-not-supportedbr"></a>Czy jakiekolwiek atrybuty folderu pamięci podręcznej nie są obsługiwane?<br/>
Następujące atrybuty folderu pamięci podręcznej ani ich kombinacje nie są obsługiwane:

* Zaszyfrowane
* Deduplikowane
* Skompresowane
* Rozrzedzone
* Punkt ponownej analizy

Folder pamięci podręcznej i dysk VHD metadanych nie mają wymaganych atrybutów dla agenta usługi Azure Backup.

### <a name="is-there-a-way-to-adjust-the-amount-of-bandwidth-used-by-the-backup-servicebr"></a>Czy istnieje sposób dostosowania wielkości przepustowości, która będzie używana przez usługę Backup?<br/>
  Tak, aby ustawić przepustowość, należy skorzystać z opcji **Zmień właściwości** agenta kopii zapasowej. Możesz dostosować wielkość przepustowości oraz czas, w którym będzie ona używana. Aby uzyskać instrukcje krok po kroku, zobacz **[Enable network throttling](backup-configure-vault.md#enable-network-throttling)** (Włączanie ograniczania użycia sieci).

## <a name="manage-backups"></a>Zarządzanie kopiami zapasowymi
### <a name="what-happens-if-i-rename-a-windows-server-that-is-backing-up-data-to-azurebr"></a>Co się stanie, jeśli zostanie zmieniona nazwa serwera Windows, który wykonuje kopie zapasowe danych na platformie Azure?<br/>
Po zmianie nazwy serwera wszystkie aktualnie skonfigurowane kopie zapasowe są zatrzymywane.
Zarejestruj nową nazwę serwera w magazynie usługi Backup. Po zarejestrowaniu nowej nazwy w magazynie pierwszą operacją kopii zapasowej będzie *pełna* kopia zapasowa. Dane, których kopia zapasowa wykonana przy użyciu starej nazwy serwera znajduje się w magazynie, można odzyskać przy użyciu opcji [**Inny serwer**](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) w kreatorze **Odtwarzanie danych**.

### <a name="what-is-the-maximum-file-path-length-that-can-be-specified-in-backup-policy-using-azure-backup-agent-br"></a>Jaka jest maksymalna długość ścieżki pliku, którą można określić w ramach zasad usługi Backup przy użyciu agenta usługi Azure Backup? <br/>
Agent usługi Azure Backup bazuje na systemie plików NTFS. [Specyfikacja długości ścieżki pliku jest ograniczona przez interfejs API systemu Windows](https://msdn.microsoft.com/library/aa365247.aspx#fully_qualified_vs._relative_paths). Jeśli długość ścieżki pliku plików, które chcesz chronić, jest większa niż dozwolona przez interfejs API systemu Windows, utwórz kopię zapasową folderu nadrzędnego lub napędu dyskowego.  

### <a name="what-characters-are-allowed-in-file-path-of-azure-backup-policy-using-azure-backup-agent-br"></a>Jakie znaki są dozwolone w ścieżce pliku zasad usługi Azure Backup przy użyciu agenta usługi Azure Backup? <br>
 Agent usługi Azure Backup bazuje na systemie plików NTFS. Dopuszcza [znaki obsługiwane w systemie NTFS](https://msdn.microsoft.com/library/aa365247.aspx#naming_conventions) w ramach specyfikacji pliku. 
 
### <a name="i-receive-the-warning-azure-backups-have-not-been-configured-for-this-server-even-though-i-configured-a-backup-policy-br"></a>Nawet po skonfigurowaniu zasad kopii zapasowych wyświetlany jest komunikat ostrzegawczy „Proces tworzenia kopii zapasowych Azure nie został skonfigurowany dla tego serwera” <br/>
Ostrzeżenie to występuje, gdy ustawienia harmonogramu tworzenia kopii zapasowych przechowywane na serwerze lokalnym nie są takie same jak ustawienia przechowywane w magazynie kopii zapasowych. Gdy serwer lub ustawienia zostały odzyskane do znanego, dobrego stanu, harmonogramy tworzenia kopii zapasowych mogą utracić synchronizację. W przypadku wystąpienia tego ostrzeżenia należy [zmienić konfigurację zasad tworzenia kopii zapasowej](backup-azure-manage-windows-server.md), a następnie wybrać opcję **Wykonaj kopię zapasową**, aby ponownie zsynchronizować lokalny serwer z platformą Azure.
