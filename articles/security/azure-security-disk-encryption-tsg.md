---
title: "Rozwiązywanie problemów z szyfrowania dysku aaaAzure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera wskazówki dotyczące rozwiązywania problemów dla programu Microsoft Azure dysku szyfrowanie dla systemu Windows i maszyn wirtualnych systemu Linux IaaS."
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: ce0e23bd-07eb-43af-a56c-aa1a73bdb747
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: devtiw
ms.openlocfilehash: 2ecb8df1fb869e3bf8f3be4be4494e6485e75695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-troubleshooting-guide"></a>Przewodnik rozwiązywania problemów szyfrowania dysków Azure

Ten przewodnik jest przeznaczony dla specjalistów technologii informatycznych (IT), informacje analityków zabezpieczeń i administratorów chmury, których organizacje używany szyfrowania dysków Azure i nie jest wymagane szyfrowanie dysków wskazówki tootroubleshoot problemy związane z.

## <a name="troubleshooting-linux-os-disk-encryption"></a>Rozwiązywanie problemów z szyfrowania dysku systemu operacyjnego Linux

Szyfrowanie dysków systemu operacyjnego Linux należy odinstalować poprzednie toorunning dysku hello systemu operacyjnego przy użyciu procesu szyfrowania dysku pełne hello.   Jeśli nie, komunikat o błędzie z "nie powiodło się toounmount po..." komunikat o błędzie jest prawdopodobnie toooccur.

Jest to najprawdopodobniej Próba szyfrowania dysku systemu operacyjnego w środowisku maszyny Wirtualnej docelowego, który został zmodyfikowany lub zmieniła się z jego obrazu obsługiwane galerii standardowych.  Przykłady odchylenia od hello obsługiwane obrazu, który może zakłócać hello rozszerzenie możliwości toounmount hello systemu operacyjnego dysku:
- Niestandardowe obrazy zgodne nie jest już obsługiwany system plików i/lub schemat partycjonowania.
- Dostosowany obraz z aplikacji, takich jak oprogramowanie antywirusowe, Docker, SAP, bazy danych MongoDB lub Cassandra Apache uruchomionych w tooencryption wcześniejsze hello systemu operacyjnego.  Te aplikacje są trudne tooterminate, a gdy zachowują dysku toohello systemu operacyjnego dojść otwartych plików hello dysk nie może zostać odinstalowane, co powoduje błąd.
- Skrypty niestandardowe, które są uruchamiane w Zamknij czas bliskości toohello szyfrowania kroku może kolidować i tego błędu. Może to nastąpić, gdy szablonu usługi Resource Manager definiuje jednocześnie wiele rozszerzeń tooexecute lub gdy rozszerzenia niestandardowego skryptu lub innych działań jest uruchamiane jednocześnie toodisk szyfrowania.   Serializację i izolowanie tych czynności może rozwiązać problem hello.
- Gdy SELinux nie było wyłączone przed tooenabling szyfrowania, hello odinstalować krok zakończy się niepowodzeniem.  SELinux można ją ponownie włączyć po ukończeniu szyfrowania.
- Gdy dysk systemu operacyjnego hello jest przy użyciu schematu LVM (mimo że dostępna jest ograniczona obsługa dysku danych LVM, dysk systemu operacyjnego LVM nie jest)
- Jeśli nie są spełnione wymagania minimalnej ilości pamięci (7GB jest zalecane do szyfrowania dysku systemu operacyjnego)
- Gdy dyski zostały rekursywnie zainstalowanego w ramach katalogu /mnt/ lub wzajemnie (na przykład /mnt/data1, /mnt/data2, /data3 + /data3/data4 itp.)
- Gdy inne szyfrowania dysków Azure [wymagania wstępne](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) dla systemu Linux nie są spełnione

## <a name="unable-tooencrypt"></a>Nie można tooencrypt

W niektórych przypadkach szyfrowanie dysków Linux hello pojawia się toobe zablokowana na "Rozpoczęto szyfrowania dysku systemu operacyjnego" i SSH jest wyłączona. Ten proces może potrwać od toocomplete 3-16 godzin na standardowych galerii.  Jeśli zostaną dodane dyski danych o rozmiarze wielu TB, hello może potrwać dni. Hello sekwencji szyfrowania dysku systemu operacyjnego Linux tymczasowo odinstalowuje dysku hello systemu operacyjnego i wykonuje szyfrowanie blok po bloku hello cały dysk systemu operacyjnego, przed woluminom on w stanie zaszyfrowane.   W odróżnieniu od szyfrowania dysków Azure w systemie Windows Linux szyfrowanie dysków nie zezwala współbieżne używanie hello maszyny Wirtualnej, gdy hello szyfrowanie jest w toku.  charakterystyki wydajności Hello hello maszyny Wirtualnej, tym hello rozmiar dysku hello i czy konto magazynu hello jest obsługiwana przez standard lub premium magazynu (SSD), znacznie może mieć wpływ hello czas toocomplete szyfrowania.

Stan toocheck pola postępu hello zwrócony z hello [Get AzureRmVmDiskEncryptionStatus](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) polecenie może być sondowane.   Dysk hello systemu operacyjnego jest szyfrowany, gdy hello wirtualna przechodzi do stanu obsługi i SSH jest również wyłączone tooprevent żadnych przerw w działaniu toohello ciągły proces.  EncryptionInProgress będą raportowane dla hello większość czasu hello podczas szyfrowania jest w toku, a następnie kilka godzin później z VMRestartPending komunikat z prośbą hello toorestart maszyny Wirtualnej.  Na przykład:


```
PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : EncryptionInProgress
DataVolumesEncrypted       : EncryptionInProgress
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk encryption started

PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : VMRestartPending
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk successfully encrypted, please reboot hello VM
```

Po wyświetleniu hello tooreboot maszyny Wirtualnej, i po ponownym hello maszyny Wirtualnej i podając 2 – 3 minuty dla hello ponowne uruchomienie komputera i toobe ostatnie kroki wykonywane w celu hello, komunikat o stanie hello będzie wskazuje, że że szyfrowanie finally zostało ukończone.   Ten komunikat jest dostępny, hello zaszyfrowany dysk systemu operacyjnego po oczekiwanym toobe gotowe do użycia i toobe wirtualna hello można używać ponownie.

W przypadkach, gdy ta sekwencja nie była widoczna lub jeśli informacje rozruchowe, komunikat o postępie lub innych wskaźników błędów zgłosić, że szyfrowanie systemu operacyjnego nie powiodła się w środku hello tego procesu (na przykład jeśli pojawia się błąd "nie powiodło się toounmount" hello opisane w tym przewodniku) Zaleca się toorestore hello wirtualna wstecz toohello migawki lub kopię zapasową wykonaną zaraz przed tooencryption.  Toohello przed ponowieniem próby jest sugerowany toore-oceny charakterystyki hello hello maszyny Wirtualnej i upewnij się, że są spełnione wszystkie wymagania wstępne.

## <a name="troubleshooting-azure-disk-encryption-behind-a-firewall"></a>Rozwiązywanie problemów z szyfrowania dysków Azure za zaporą
Gdy łączność jest ograniczone przez zapory, wymagania serwera proxy lub ustawienia Grupa zabezpieczeń sieci zdolność hello tooperform rozszerzenia hello wymagane zadania mogą być zakłócona.   Może to spowodować komunikaty stanu, takie jak "Stan rozszerzenia nie jest dostępny na powitania maszyny Wirtualnej" w oczekiwanym scenariuszy awarii toofinish.  kolejnych sekcjach Hello ma niektórych typowych problemów zapory, które mogą zbadać.

### <a name="network-security-groups"></a>Grupy zabezpieczeń sieci
Wszystkie ustawienia grupy zabezpieczeń sieci stosowane nadal muszą zezwalać konfiguracji sieci hello udokumentowane hello punktu końcowego toomeet [wymagania wstępne](https://docs.microsoft.com/azure/security/azure-security-disk-encryption#prerequisites) szyfrowanie dysków.

### <a name="azure-keyvault-behind-firewall"></a>Azure Keyvault za zaporą
Hello maszyny Wirtualnej musi być możliwe tooaccess magazynu kluczy. Zobacz tooguidance po błędzie tookey dostępu za zaporą, która jest obsługiwana przez hello [Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-access-behind-firewall) zespołu.

### <a name="linux-package-management-behind-firewall"></a>Linux zarządzania pakietami za zaporą
W czasie wykonywania szyfrowania dysków Azure dla systemu Linux zależy od hello docelowy dystrybucji pakietu zarządzania systemu tooinstall wymagane wstępnie wymagane składniki wcześniejsze tooenabling szyfrowania.  Jeśli ustawienia zapory uniemożliwiają hello maszyna wirtualna stanie toodownload i zainstalować te składniki, kolejne błędy są oczekiwane.    Hello tooconfigure kroki, które to mogą różnić się o dystrybucji.  Na Red Hat gdy serwer proxy jest wymagany, zapewnienie, że Menedżer subskrypcji i yum są prawidłowo skonfigurowane jest niezbędne.  Zobacz [to](https://access.redhat.com/solutions/189533) Red Hat artykuł pomocy technicznej dotyczące tego tematu.  

## <a name="troubleshooting-windows-server-2016-server-core"></a>Rozwiązywanie problemów z systemem Windows Server 2016 Server Core

W systemie Windows Server 2016 Server Core hello bdehdcfg składnik nie jest dostępny domyślnie. Ten składnik jest wymagany przez szyfrowanie dysków Azure.

tooworkaround ten problem, hello kopiowania następujące 4 pliki z folderu c:\windows\system32 toohello maszyny Wirtualnej centrum danych systemu Windows Server 2016 hello Server Core obrazu:

```
bdehdcfg.exe
bdehdcfglib.dll
bdehdcfglib.dll.mui
bdehdcfg.exe.mui
```

Następnie uruchom następujące polecenie hello:

```
bdehdcfg.exe -target default
```

Spowoduje to utworzenie partycji systemowej 550MB, a następnie po ponownym uruchomieniu, można użyć narzędzia Diskpart toocheck hello woluminów i kontynuować.  

Na przykład:

```
DISKPART> list vol

  Volume ###  Ltr  Label        Fs     Type        Size     Status     Info
  ----------  ---  -----------  -----  ----------  -------  ---------  --------
  Volume 0     C                NTFS   Partition    126 GB  Healthy    Boot
  Volume 1                      NTFS   Partition    550 MB  Healthy    System
  Volume 2     D   Temporary S  NTFS   Partition     13 GB  Healthy    Pagefile
```
## <a name="see-also"></a>Zobacz też
W tym dokumencie przedstawiono więcej informacji na temat niektórych typowych problemów w przypadku szyfrowania dysków Azure i w jaki sposób tootroubleshoot. Aby uzyskać więcej informacji na temat tej usługi i jego możliwości odczytu:

- [Zastosuj szyfrowanie dysków w Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [Szyfrowanie maszyny wirtualnej platformy Azure](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Danych Azure szyfrowania na Rest](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)
