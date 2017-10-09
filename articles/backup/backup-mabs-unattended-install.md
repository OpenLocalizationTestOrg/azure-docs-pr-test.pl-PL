---
title: "aaaSilent instalacji serwera usługi Kopia zapasowa Azure w wersji 2 | Dokumentacja firmy Microsoft"
description: "Użycie toosilently skrypt programu PowerShell zainstalowanie serwer kopii zapasowej Azure w wersji 2. Ten rodzaj instalacji jest również nazywany instalacji nienadzorowanej."
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/30/2017
ms.author: markgal;masaran
ms.openlocfilehash: 6b94b4a278bfcd5f8c5c363cb811bd8eec984243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a>Uruchamianie nienadzorowanej instalacji serwera usługi Kopia zapasowa Azure w wersji 2

Dowiedz się, jak toorun instalacji nienadzorowanej v2 serwer kopii zapasowej Azure. 

Te kroki nie są stosowane, jeśli instalujesz serwer kopii zapasowej Azure w wersji 1.

## <a name="install-backup-server-v2"></a>Zainstaluj serwer zapasowy v2

1. Na serwerze hello, który jest hostem serwera usługi Kopia zapasowa Azure w wersji 2 Utwórz plik tekstowy. (Można utworzyć pliku hello w Notatniku lub w innym tekście edytora.) Zapisz plik hello jako MABSSetup.ini. 

2. Wklej hello następującego kodu w pliku MABSSetup.ini hello. Zastąp tekst hello w nawiasach hello (\< \>) z wartościami z używanego środowiska. Przykładem jest Hello następującego tekstu:

  ```
  [OPTIONS]
  UserName=administrator
  CompanyName=<Microsoft Corporation>
  SQLMachineName=localhost
  SQLInstanceName=<SQL instance name>
  SQLMachineUserName=administrator
  SQLMachinePassword=<admin password>
  SQLMachineDomainName=<machine domain>
  ReportingMachineName=localhost
  ReportingInstanceName=<reporting instance name>
  SqlAccountPassword=<admin password>
  ReportingMachineUserName=<username>
  ReportingMachinePassword=<reporting admin password>
  ReportingMachineDomainName=<domain>
  VaultCredentialFilePath=<vault credential full path and complete name>
  SecurityPassphrase=<passphrase>
  PassphraseSaveLocation=<passphrase save location>
  UseExistingSQL=<1/0 use or do not use existing SQL>
  ```

3. Zapisz plik hello. Następnie w wierszu polecenia z podwyższonym poziomem uprawnień na serwerze instalacji hello, wprowadź polecenie:

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

Można użyć tych flag do instalacji hello:</br>
**/f**: ścieżka pliku ini</br>
**/l**: ścieżka dziennika</br>
**/i**: ścieżka instalacji</br>
**/x**: Odinstaluj ścieżki</br>

## <a name="next-steps"></a>Następne kroki
Po zainstalowaniu serwera kopii zapasowej, Dowiedz się jak tooprepare serwera, lub Włącz ochronę obciążeń.

- [Przygotowanie serwera kopii zapasowej obciążeń](backup-azure-microsoft-azure-backup.md)
- [Użyj tooback serwera kopii zapasowej serwera VMware](backup-azure-backup-server-vmware.md)
- [Użyj tooback serwera kopii zapasowej serwera SQL](backup-azure-sql-mabs.md)
- [Dodaj tooBackup nowoczesnych magazynu kopii zapasowej serwera](backup-mabs-add-storage.md)
