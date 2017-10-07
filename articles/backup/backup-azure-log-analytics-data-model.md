---
title: "model danych Analytics aaaLog dla usługi Kopia zapasowa Azure"
description: "Ten artykuł zawiera informacje o szczegóły modelu danych analizy dzienników dla danych kopii zapasowej Azure."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: dfd5c73d-0d34-4d48-959e-1936986f9fc0
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 04ac16e38b896851f60b1c4ffbea4343347ae32c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-data-model-for-azure-backup-data"></a>Model danych analizy dziennika dla danych kopia zapasowa Azure
W tym artykule opisano model danych hello używane do raportowania danych tooLog Analytics wypychania. Użycie tego modelu danych, można tworzyć zapytania niestandardowe pulpity nawigacyjne i wykorzystanie go w OMS. 

## <a name="using-azure-backup-data-model"></a>Za pomocą usługi Kopia zapasowa Azure modelu danych
Możesz użyć hello kolejnych pól w ramach hello danych modelu toocreate wizualnych, niestandardowych kwerend i pulpitu nawigacyjnego zgodnie z wymaganiami.

### <a name="alert"></a>Alerty
Ta tabela zawiera szczegóły dotyczące alertu związane pola.

| Pole | Typ danych | Opis |
| --- | --- | --- |
| AlertUniqueId_s |Tekst |Unikatowy identyfikator hello wygenerowany alert |
| AlertType_s |Tekst |Typ hello wygenerowany alert, na przykład kopii zapasowej |
| AlertStatus_s |Tekst |Stan alertu hello, na przykład aktywny |
| AlertOccurenceDateTime_s |Data i godzina |Data i godzina utworzenia alertu |
| AlertSeverity_s |Tekst |Ważność alertu hello, na przykład krytyczne |
| EventName_s |Tekst |To pole reprezentuje nazwę tego zdarzenia, jest zawsze AzureBackupCentralReport |
| BackupItemUniqueId_s |Tekst |Unikatowy identyfikator hello toowhich kopii zapasowej elementu, którego należy ten alert|
| SchemaVersion_s |Tekst |To pole określa bieżąca wersja schematu hello, jest **V1** |
| State_s |Tekst |Bieżący stan obiektu alertu hello, na przykład aktywny, usunięte |
| BackupManagementType_s |Tekst |Typ dostawcy do wykonywania kopii zapasowej, na przykład IaaSVM toowhich FileFolder, do którego należy ten alert|
| OperationName |Tekst |To pole reprezentuje nazwę hello bieżącej operacji - alertu |
| Kategoria |Tekst |To pole reprezentuje kategorię danych diagnostycznych wypychana tooLog Analytics, jest AzureBackupReport |
| Zasób |Tekst |Jest to hello zasobu, dla którego dane są zbierane, będzie wyświetlana nazwa magazynu usług odzyskiwania |
| ProtectedServerUniqueId_s |Tekst |Unikatowy identyfikator hello chronione toowhich, do którego należy ten alert|
| VaultUniqueId_s |Tekst |Unikatowy identyfikator hello chronione toowhich, do którego należy ten alert|
| SourceSystem |Tekst |System źródła danych bieżącego hello - Azure |
| Identyfikator zasobu |Tekst |To pole reprezentuje identyfikator zasobu dla którego dane są zbierane, zawiera identyfikator zasobu magazynu usług odzyskiwania |
| SubscriptionId |Tekst |To pole reprezentuje identyfikator subskrypcji zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceGroup |Tekst |To pole reprezentuje grupę zasobów zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceProvider |Tekst |To pole reprezentuje hello dostawcy zasobów dla których są zbierane dane - Microsoft.RecoveryServices |
| ResourceType |Tekst |To pole reprezentuje typ hello zasobów, dla których są zbierane dane — magazynów |

### <a name="backupitem"></a>BackupItem
Ta tabela zawiera szczegółowe informacje dotyczące tworzenia kopii zapasowej pól związanych z elementu.

| Pole | Typ danych | Opis |
| --- | --- | --- |
| EventName_s |Tekst |To pole reprezentuje nazwę tego zdarzenia, jest zawsze AzureBackupCentralReport |  
| BackupItemUniqueId_s |Tekst |Unikatowy identyfikator elementu kopii zapasowej hello |
| BackupItemId_s |Tekst |Identyfikator elementu kopii zapasowej |
| BackupItemName_s |Tekst |Nazwa elementu kopii zapasowej |
| BackupItemFriendlyName_s |Tekst |Przyjazna nazwa elementu kopii zapasowej |
| BackupItemType_s |Tekst |Typ elementu kopii zapasowej, na przykład maszynę Wirtualną, FileFolder |
| ProtectedServerName_s |Tekst |Nazwa elementu kopii zapasowych serwera chronionego toowhich należy|
| ProtectionState_s |Tekst |Bieżący stan ochrony hello elementu kopii zapasowej, na przykład chronione, ProtectionStopped |
| SchemaVersion_s |Tekst |To pole określa bieżąca wersja schematu hello, jest **V1** |
| State_s |Tekst |Bieżący stan obiektu kopii zapasowej elementu hello, na przykład aktywny, usunięte |
| BackupManagementType_s |Tekst |Typ dostawcy do wykonywania kopii zapasowej, na przykład IaaSVM toowhich FileFolder, którego ten element kopii zapasowej należy|
| OperationName |Tekst |To pole reprezentuje nazwę hello bieżącej operacji - BackupItem |
| Kategoria |Tekst |To pole reprezentuje kategorię danych diagnostycznych wypychana tooLog Analytics, jest AzureBackupReport |
| Zasób |Tekst |Jest to hello zasobu, dla którego dane są zbierane, będzie wyświetlana nazwa magazynu usług odzyskiwania |
| SourceSystem |Tekst |System źródła danych bieżącego hello - Azure |
| Identyfikator zasobu |Tekst |To pole reprezentuje identyfikator zasobu dla którego dane są zbierane, zawiera identyfikator zasobu magazynu usług odzyskiwania |
| SubscriptionId |Tekst |To pole reprezentuje identyfikator subskrypcji zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceGroup |Tekst |To pole reprezentuje grupę zasobów zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceProvider |Tekst |To pole reprezentuje hello dostawcy zasobów dla których są zbierane dane - Microsoft.RecoveryServices |
| ResourceType |Tekst |To pole reprezentuje typ hello zasobów, dla których są zbierane dane — magazynów |

### <a name="backupitemassociation"></a>BackupItemAssociation
Ta tabela zawiera szczegółowe informacje dotyczące skojarzenia elementu kopii zapasowej z różnymi jednostkami.

| Pole | Typ danych | Opis |
| --- | --- | --- |
| EventName_s |Tekst |To pole reprezentuje nazwę tego zdarzenia, jest zawsze AzureBackupCentralReport |  
| BackupItemUniqueId_s |Tekst |Unikatowy identyfikator elementu kopii zapasowej hello |
| SchemaVersion_s |Tekst |To pole określa bieżąca wersja schematu hello, jest **V1** |
| State_s |Tekst |Bieżący stan hello elementu kopii zapasowej skojarzenie obiektu, na przykład aktywny, usunięte |
| BackupManagementType_s |Tekst |Typ dostawcy do wykonywania kopii zapasowej, na przykład IaaSVM toowhich FileFolder, którego ten element kopii zapasowej należy|
| OperationName |Tekst |To pole reprezentuje nazwę hello bieżącej operacji - BackupItemAssociation |
| Kategoria |Tekst |To pole reprezentuje kategorię danych diagnostycznych wypychana tooLog Analytics, jest AzureBackupReport |
| Zasób |Tekst |Jest to hello zasobu, dla którego dane są zbierane, będzie wyświetlana nazwa magazynu usług odzyskiwania |
| PolicyUniqueId_g |Tekst |Unikatowy identyfikator tooidentify hello zasad, które kopii zapasowej jest skojarzony element zbyt|
| ProtectedServerUniqueId_s |Tekst |Unikatowy identyfikator hello chronione toowhich serwer, którego ten element kopii zapasowej należy|
| VaultUniqueId_s |Tekst |Unikatowy identyfikator hello toowhich magazynu, którego ten element kopii zapasowej należy|
| SourceSystem |Tekst |System źródła danych bieżącego hello - Azure |
| Identyfikator zasobu |Tekst |To pole reprezentuje identyfikator zasobu dla którego dane są zbierane, zawiera identyfikator zasobu magazynu usług odzyskiwania |
| SubscriptionId |Tekst |To pole reprezentuje identyfikator subskrypcji zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceGroup |Tekst |To pole reprezentuje grupę zasobów zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceProvider |Tekst |To pole reprezentuje hello dostawcy zasobów dla których są zbierane dane - Microsoft.RecoveryServices |
| ResourceType |Tekst |To pole reprezentuje typ hello zasobów, dla których są zbierane dane — magazynów |

### <a name="job"></a>Zadanie
Ta tabela zawiera szczegółowe informacje o polach związanych z pracą.

| Pole | Typ danych | Opis |
| --- | --- | --- |
| EventName_s |Tekst |To pole reprezentuje nazwę tego zdarzenia, jest zawsze AzureBackupCentralReport |
| BackupItemUniqueId_s |Tekst |Unikatowy identyfikator hello toowhich elementu kopii zapasowej, której to zadanie należy zbyt|
| SchemaVersion_s |Tekst |To pole określa bieżąca wersja schematu hello, jest **V1** |
| State_s |Tekst |Bieżący stan obiektu zadania hello, na przykład aktywny, usunięte |
| BackupManagementType_s |Tekst |Typ dostawcy do wykonywania kopii zapasowej, na przykład IaaSVM toowhich FileFolder, której to zadanie należy zbyt|
| OperationName |Tekst |To pole reprezentuje nazwę bieżącej operacji hello — zadanie |
| Kategoria |Tekst |To pole reprezentuje kategorię danych diagnostycznych wypychana tooLog Analytics, jest AzureBackupReport |
| Zasób |Tekst |Jest to hello zasobu, dla którego dane są zbierane, będzie wyświetlana nazwa magazynu usług odzyskiwania |
| ProtectedServerUniqueId_s |Tekst |Unikatowy identyfikator hello chronione toowhich, której to zadanie należy zbyt|
| VaultUniqueId_s |Tekst |Unikatowy identyfikator hello chronione toowhich, której to zadanie należy zbyt|
| JobOperation_s |Tekst |Operacja, dla którego zadanie jest uruchamiane na przykład kopii zapasowych, przywracania, konfigurowanie usługi Kopia zapasowa |
| JobStatus_s |Tekst |Stan hello zakończył zadanie, na przykład ukończone, nie powiodło się |
| JobFailureCode_s |Tekst |Ciąg kodu błędu z powodu którego wystąpiło niepowodzenie zadania |
| JobStartDateTime_s |Data i godzina |Data i godzina podczas zadań uruchomiona wprowadzenie |
| BackupStorageDestination_s |Tekst |Miejsce docelowe magazynu kopii zapasowej, na przykład chmury, dysku  |
| JobDurationInSecs_s | Liczba |Zadanie całkowity czas w sekundach |
| DataTransferredInMB_s | Liczba |Dane przekazywane w MB dla tego zadania|
| JobUniqueId_g |Tekst |Unikatowy identyfikator tooidentify hello zadania |
| SourceSystem |Tekst |System źródła danych bieżącego hello - Azure |
| Identyfikator zasobu |Tekst |To pole reprezentuje identyfikator zasobu dla którego dane są zbierane, zawiera identyfikator zasobu magazynu usług odzyskiwania |
| SubscriptionId |Tekst |To pole reprezentuje identyfikator subskrypcji zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceGroup |Tekst |To pole reprezentuje grupę zasobów zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceProvider |Tekst |To pole reprezentuje hello dostawcy zasobów dla których są zbierane dane - Microsoft.RecoveryServices |
| ResourceType |Tekst |To pole reprezentuje typ hello zasobów, dla których są zbierane dane — magazynów |

### <a name="policy"></a>Zasady
Ta tabela zawiera szczegółowe informacje o polach związane z zasadami.

| Pole | Typ danych | Opis |
| --- | --- | --- |
| EventName_s |Tekst |To pole reprezentuje nazwę tego zdarzenia, jest zawsze AzureBackupCentralReport |
| SchemaVersion_s |Tekst |To pole określa bieżąca wersja schematu hello, jest **V1** |
| State_s |Tekst |Bieżący stan obiektu zasad hello, na przykład aktywny, usunięte |
| BackupManagementType_s |Tekst |Typ dostawcy do wykonywania kopii zapasowej, na przykład IaaSVM toowhich FileFolder, do którego należy ta zasada|
| OperationName |Tekst |To pole reprezentuje nazwę hello bieżącej operacji — zasady |
| Kategoria |Tekst |To pole reprezentuje kategorię danych diagnostycznych wypychana tooLog Analytics, jest AzureBackupReport |
| Zasób |Tekst |Jest to hello zasobu, dla którego dane są zbierane, będzie wyświetlana nazwa magazynu usług odzyskiwania |
| PolicyUniqueId_g |Tekst |Unikatowy identyfikator tooidentify hello zasad |
| PolicyName_s |Tekst |Nazwa zasad hello zdefiniowany |
| BackupFrequency_s |Tekst |Częstotliwość, z którym są uruchamiane kopii zapasowych, na przykład, codziennie, co tydzień |
| BackupTimes_s |Tekst |Data i godzina, kiedy zaplanowane tworzenie kopii zapasowych |
| BackupDaysOfTheWeek_s |Tekst |Dni tygodnia hello podczas zaplanowanych kopii zapasowych |
| RetentionDuration_s |Liczby całkowitej |Czas przechowywania kopii zapasowych skonfigurowany |
| DailyRetentionDuration_s |Liczby całkowitej |Czas trwania całkowita przechowywania w dniach skonfigurowanych kopii zapasowych |
| DailyRetentionTimes_s |Tekst |Data i godzina, gdy skonfigurowano przechowywania codziennych |
| WeeklyRetentionDuration_s |Liczba dziesiętna |Całkowita liczba tygodniowy czas przechowywania w tygodniach skonfigurowanych kopii zapasowych |
| WeeklyRetentionTimes_s |Tekst |Data i godzina, gdy jest skonfigurowany co tydzień przechowywania |
| WeeklyRetentionDaysOfTheWeek_s |Tekst |Wybrane dni tygodnia hello do przechowywania co tydzień |
| MonthlyRetentionDuration_s |Liczba dziesiętna |Czas przechowywania całkowitej w miesiącach skonfigurowanych kopii zapasowych |
| MonthlyRetentionTimes_s |Tekst |Data i godzina, gdy miesięczne przechowywania jest skonfigurowany |
| MonthlyRetentionFormat_s |Tekst |Typ konfiguracji miesięczne okresu przechowywania, na przykład codziennie na podstawie co tydzień na podstawie tydzień dzień |
| MonthlyRetentionDaysOfTheWeek_s |Tekst |Wybrane dni tygodnia hello do przechowywania miesięcznego |
| MonthlyRetentionWeeksOfTheMonth_s |Tekst |Tygodnie miesiąca hello podczas przechowywania miesięcznych jest skonfigurowany, na przykład pierwszy, ostatni itp. |
| YearlyRetentionDuration_s |Liczba dziesiętna |Czas przechowywania całkowitej w latach skonfigurowanych kopii zapasowych |
| YearlyRetentionTimes_s |Tekst |Data i godzina, gdy corocznych przechowywania jest skonfigurowany |
| YearlyRetentionMonthsOfTheYear_s |Tekst |Miesięcy roku hello wybrany do przechowywania roczne |
| YearlyRetentionFormat_s |Tekst |Typ konfiguracji corocznych okresu przechowywania, na przykład codziennie na podstawie co tydzień na podstawie tydzień dzień |
| YearlyRetentionDaysOfTheMonth_s |Tekst |Daty miesiąca hello wybrany do przechowywania roczne |
| SourceSystem |Tekst |System źródła danych bieżącego hello - Azure |
| Identyfikator zasobu |Tekst |To pole reprezentuje identyfikator zasobu dla którego dane są zbierane, zawiera identyfikator zasobu magazynu usług odzyskiwania |
| SubscriptionId |Tekst |To pole reprezentuje identyfikator subskrypcji zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceGroup |Tekst |To pole reprezentuje grupę zasobów zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceProvider |Tekst |To pole reprezentuje hello dostawcy zasobów dla których są zbierane dane - Microsoft.RecoveryServices |
| ResourceType |Tekst |To pole reprezentuje typ hello zasobów, dla których są zbierane dane — magazynów |

### <a name="policyassociation"></a>PolicyAssociation
Ta tabela zawiera szczegółowe informacje dotyczące skojarzenia zasad z różnymi jednostkami.

| Pole | Typ danych | Opis |
| --- | --- | --- |
| EventName_s |Tekst |To pole reprezentuje nazwę tego zdarzenia, jest zawsze AzureBackupCentralReport |
| SchemaVersion_s |Tekst |To pole określa bieżąca wersja schematu hello, jest **V1** |
| State_s |Tekst |Bieżący stan obiektu zasad hello, na przykład aktywny, usunięte |
| BackupManagementType_s |Tekst |Typ dostawcy do wykonywania kopii zapasowej, na przykład IaaSVM toowhich FileFolder, do którego należy ta zasada|
| OperationName |Tekst |To pole reprezentuje nazwę hello bieżącej operacji - PolicyAssociation |
| Kategoria |Tekst |To pole reprezentuje kategorię danych diagnostycznych wypychana tooLog Analytics, jest AzureBackupReport |
| Zasób |Tekst |Jest to hello zasobu, dla którego dane są zbierane, będzie wyświetlana nazwa magazynu usług odzyskiwania |
| PolicyUniqueId_g |Tekst |Unikatowy identyfikator tooidentify hello zasad |
| VaultUniqueId_s |Tekst |Unikatowy identyfikator hello toowhich magazynu, którego należy ta zasada|
| SourceSystem |Tekst |System źródła danych bieżącego hello - Azure |
| Identyfikator zasobu |Tekst |To pole reprezentuje identyfikator zasobu dla którego dane są zbierane, zawiera identyfikator zasobu magazynu usług odzyskiwania |
| SubscriptionId |Tekst |To pole reprezentuje identyfikator subskrypcji zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceGroup |Tekst |To pole reprezentuje grupę zasobów zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceProvider |Tekst |To pole reprezentuje hello dostawcy zasobów dla których są zbierane dane - Microsoft.RecoveryServices |
| ResourceType |Tekst |To pole reprezentuje typ hello zasobów, dla których są zbierane dane — magazynów |

### <a name="protectedserver"></a>ProtectedServer
Ta tabela zawiera szczegółowe informacje o chronionych polach związanych z serwerem.

| Pole | Typ danych | Opis |
| --- | --- | --- |
| EventName_s |Tekst |To pole reprezentuje nazwę tego zdarzenia, jest zawsze AzureBackupCentralReport |
| ProtectedServerName_s |Tekst |Nazwa serwera chronionego |
| SchemaVersion_s |Tekst |To pole określa bieżąca wersja schematu hello, jest **V1** |
| State_s |Tekst |Bieżący stan hello chronionego obiektu serwera, na przykład aktywny, usunięte |
| BackupManagementType_s |Tekst |Typ dostawcy do wykonywania kopii zapasowej, na przykład IaaSVM toowhich FileFolder, do którego należy ten serwer chroniony za|
| OperationName |Tekst |To pole reprezentuje nazwę hello bieżącej operacji - ProtectedServer |
| Kategoria |Tekst |To pole reprezentuje kategorię danych diagnostycznych wypychana tooLog Analytics, jest AzureBackupReport |
| Zasób |Tekst |Jest to hello zasobu, dla którego dane są zbierane, będzie wyświetlana nazwa magazynu usług odzyskiwania |
| ProtectedServerUniqueId_s |Tekst |Unikatowy identyfikator hello serwerze chronionym |
| RegisteredContainerId_s |Tekst |Identyfikator kontenera zarejestrowany dla kopii zapasowej |
| ProtectedServerType_s |Tekst |Typ serwera chronionego kopię zapasową na przykład systemu Windows |
| ProtectedServerFriendlyName_s |Tekst |Przyjazna nazwa serwera chronionego |
| AzureBackupAgentVersion_s |Tekst |Numer wersji wersja agenta kopii zapasowej |
| SourceSystem |Tekst |System źródła danych bieżącego hello - Azure |
| Identyfikator zasobu |Tekst |To pole reprezentuje identyfikator zasobu dla którego dane są zbierane, zawiera identyfikator zasobu magazynu usług odzyskiwania |
| SubscriptionId |Tekst |To pole reprezentuje identyfikator subskrypcji zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceGroup |Tekst |To pole reprezentuje grupę zasobów zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceProvider |Tekst |To pole reprezentuje hello dostawcy zasobów dla których są zbierane dane - Microsoft.RecoveryServices |
| ResourceType |Tekst |To pole reprezentuje typ hello zasobów, dla których są zbierane dane — magazynów |

### <a name="protectedserverassociation"></a>ProtectedServerAssociation
Ta tabela zawiera szczegółowe informacje o serwerze chronionym powiązania z innych jednostek.

| Pole | Typ danych | Opis |
| --- | --- | --- |
| EventName_s |Tekst |To pole reprezentuje nazwę tego zdarzenia, jest zawsze AzureBackupCentralReport |
| SchemaVersion_s |Tekst |To pole określa bieżąca wersja schematu hello, jest **V1** |
| State_s |Tekst |Bieżący stan hello chronione skojarzenie obiektu serwera, na przykład aktywny, usunięte |
| BackupManagementType_s |Tekst |Typ dostawcy do wykonywania kopii zapasowej, na przykład IaaSVM toowhich FileFolder, do którego należy ten serwer chroniony za|
| OperationName |Tekst |To pole reprezentuje nazwę hello bieżącej operacji - ProtectedServerAssociation |
| Kategoria |Tekst |To pole reprezentuje kategorię danych diagnostycznych wypychana tooLog Analytics, jest AzureBackupReport |
| Zasób |Tekst |Jest to hello zasobu, dla którego dane są zbierane, będzie wyświetlana nazwa magazynu usług odzyskiwania |
| ProtectedServerUniqueId_s |Tekst |Unikatowy identyfikator hello serwerze chronionym |
| VaultUniqueId_s |Tekst |Unikatowy identyfikator hello toowhich magazynu, którego należy ten serwer chroniony za|
| SourceSystem |Tekst |System źródła danych bieżącego hello - Azure |
| Identyfikator zasobu |Tekst |To pole reprezentuje identyfikator zasobu dla którego dane są zbierane, zawiera identyfikator zasobu magazynu usług odzyskiwania |
| SubscriptionId |Tekst |To pole reprezentuje identyfikator subskrypcji zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceGroup |Tekst |To pole reprezentuje grupę zasobów zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceProvider |Tekst |To pole reprezentuje hello dostawcy zasobów dla których są zbierane dane - Microsoft.RecoveryServices |
| ResourceType |Tekst |To pole reprezentuje typ hello zasobów, dla których są zbierane dane — magazynów |

### <a name="storage"></a>Magazyn
Ta tabela zawiera szczegółowe informacje dotyczące pola dotyczące magazynu.

| Pole | Typ danych | Opis |
| --- | --- | --- |
| CloudStorageInBytes_s |Liczba dziesiętna |Magazynu kopii zapasowej w chmurze używane przez kopie zapasowe, które są obliczane na podstawie najnowszej wartości |
| ProtectedInstances_s |Liczba dziesiętna |Liczba służące do obliczania magazynu frontonu w rozliczeń, obliczonej na podstawie wartości najnowsze wystąpienia chronione |
| EventName_s |Tekst |To pole reprezentuje nazwę tego zdarzenia, jest zawsze AzureBackupCentralReport |
| SchemaVersion_s |Tekst |To pole określa bieżąca wersja schematu hello, jest **V1** |
| State_s |Tekst |Bieżący stan obiektu przechowywania hello, na przykład aktywny, usunięte |
| BackupManagementType_s |Tekst |Typ dostawcy do wykonywania kopii zapasowej, na przykład IaaSVM toowhich FileFolder, w której ta pamięć masowa należy zbyt|
| OperationName |Tekst |To pole reprezentuje nazwę hello bieżącej operacji — magazyn |
| Kategoria |Tekst |To pole reprezentuje kategorię danych diagnostycznych wypychana tooLog Analytics, jest AzureBackupReport |
| Zasób |Tekst |Jest to hello zasobu, dla którego dane są zbierane, będzie wyświetlana nazwa magazynu usług odzyskiwania |
| ProtectedServerUniqueId_s |Tekst |Unikatowy identyfikator hello chronionego serwera, dla którego jest obliczana magazynu |
| VaultUniqueId_s |Tekst |Unikatowy identyfikator hello magazynu dla magazynu jest obliczana. |
| SourceSystem |Tekst |System źródła danych bieżącego hello - Azure |
| Identyfikator zasobu |Tekst |To pole reprezentuje identyfikator zasobu dla którego dane są zbierane, zawiera identyfikator zasobu magazynu usług odzyskiwania |
| SubscriptionId |Tekst |To pole reprezentuje identyfikator subskrypcji zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceGroup |Tekst |To pole reprezentuje grupę zasobów zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceProvider |Tekst |To pole reprezentuje hello dostawcy zasobów dla których są zbierane dane - Microsoft.RecoveryServices |
| ResourceType |Tekst |Representse tego pola typu hello zasobów dla których są zbierane dane - magazynów |

### <a name="vault"></a>Magazyn
Ta tabela zawiera szczegółowe informacje dotyczące pola związane z magazynem.

| Pole | Typ danych | Opis |
| --- | --- | --- |
| EventName_s |Tekst |To pole reprezentuje nazwę tego zdarzenia, jest zawsze AzureBackupCentralReport |
| SchemaVersion_s |Tekst |To pole określa bieżąca wersja schematu hello, jest **V1** |
| State_s |Tekst |Bieżący stan obiektu magazynu hello, na przykład aktywny, usunięte |
| OperationName |Tekst |To pole reprezentuje nazwę hello bieżącej operacji — magazyn |
| Kategoria |Tekst |To pole reprezentuje kategorię danych diagnostycznych wypychana tooLog Analytics, jest AzureBackupReport |
| Zasób |Tekst |Jest to hello zasobu, dla którego dane są zbierane, będzie wyświetlana nazwa magazynu usług odzyskiwania |
| VaultUniqueId_s |Tekst |Unikatowy identyfikator hello magazynu |
| VaultName_s |Tekst |Nazwa magazynu hello |
| AzureDataCenter_s |Tekst |Centrum danych, w którym znajduje się magazyn |
| StorageReplicationType_s |Tekst |Typ replikacji magazynu hello magazynu, na przykład GeoRedundant |
| SourceSystem |Tekst |System źródła danych bieżącego hello - Azure |
| Identyfikator zasobu |Tekst |To pole reprezentuje identyfikator zasobu dla którego dane są zbierane, zawiera identyfikator zasobu magazynu usług odzyskiwania |
| SubscriptionId |Tekst |To pole reprezentuje identyfikator subskrypcji zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceGroup |Tekst |To pole reprezentuje grupę zasobów zasobu hello (RS magazynu), dla którego dane są zbierane |
| ResourceProvider |Tekst |To pole reprezentuje hello dostawcy zasobów dla których są zbierane dane - Microsoft.RecoveryServices |
| ResourceType |Tekst |To pole reprezentuje typ hello zasobów, dla których są zbierane dane — magazynów |

## <a name="next-steps"></a>Następne kroki
Po przejrzeniu hello modelu danych do tworzenia raportów usługi Kopia zapasowa Azure, możesz uruchomić [Tworzenie pulpitu nawigacyjnego](../log-analytics/log-analytics-dashboards.md) analizy dzienników i OMS.
