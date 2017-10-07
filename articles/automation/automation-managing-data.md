---
title: "aaaManaging danych usługi Automatyzacja Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera wiele tematów do zarządzania środowiskiem usługi Automatyzacja Azure.  Obecnie obejmuje przechowywanie danych i tworzenie kopii zapasowej odzyskiwania po awarii usługi Automatyzacja Azure w automatyzacji Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 2896f129-82e3-43ce-b9ee-a3860be0423a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/201
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: 46a164d864c4956c90ab689ca159fff6f6c08028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-automation-data"></a>Zarządzanie danymi usługi Azure Automation
Ten artykuł zawiera wiele tematów do zarządzania środowiskiem usługi Automatyzacja Azure.

## <a name="data-retention"></a>Przechowywanie danych
Kiedy usuniesz zasób w automatyzacji Azure, są przechowywane przez 90 dni na potrzeby inspekcji przed zostaną trwale usunięte.  Nie można wyświetlić lub użyj hello zasobów w tym czasie.  Ta zasada ma zastosowanie również tooresources, który należy tooan konta automatyzacji, który zostanie usunięty.

Automatyzacja Azure automatycznie usuwa i trwale starsze niż 90 dni zadania.

Witaj w poniższej tabeli przedstawiono podsumowanie hello zasad przechowywania dla różnych zasobów.

| Dane | Zasady |
|:--- |:--- |
| Konta |Trwale usunąć 90 dni, po usunięciu konta hello przez użytkownika. |
| Elementy zawartości |Trwale usunięte po upływie 90 dni po hello zasobów zostanie usunięta przez użytkownika, lub 90 dni od hello konta, które przechowuje hello zasobów zostanie usunięta przez użytkownika. |
| Moduły |Trwale usunięte po upływie 90 dni po modułu hello została usunięta przez użytkownika, lub 90 dni od hello konta, które zawiera moduł hello jest usunięty przez użytkownika. |
| Elementy Runbook |Trwale usunięte po upływie 90 dni po hello zasobów zostanie usunięta przez użytkownika, lub 90 dni od hello konta, które przechowuje hello zasobów zostanie usunięta przez użytkownika. |
| Zadania |Usunięte i trwale usunięte 90 dni od ostatniego jest modyfikowany. Może to być po zakończeniu hello zadania, jest zatrzymana lub jest wstrzymana. |
| Pliki konfiguracji/MOF węzła |Starą konfigurację węzła zostanie usunięty po upływie 90 dni po wygenerowaniu nowego konfiguracji węzła. |
| Węzły DSC |Trwale usunąć 90 dni od węzła hello jest wyrejestrowany z konta automatyzacji za pomocą portalu Azure lub hello [Unregister-AzureRMAutomationDscNode](https://msdn.microsoft.com/library/mt603500.aspx) polecenia cmdlet programu Windows PowerShell. Węzły są również trwale usuwane 90 dni od konta hello, która przetrzymuje węzeł hello jest usunięty przez użytkownika. |
| Raporty węzła |Trwale usunięte po upływie 90 dni po wygenerowaniu nowego raportu dla tego węzła |

zasady przechowywania Hello stosuje tooall użytkowników i obecnie nie można dostosować.

Jednak jeśli potrzebujesz danych tooretain dłuższy okres czasu, można przekazywać tooLog dzienniki zadania elementu runbook Analytics.  Aby uzyskać więcej informacji, przejrzyj [przekazywania tooOMS dane zadanie usługi Automatyzacja Azure Log Analytics](automation-manage-send-joblogs-log-analytics.md).   

## <a name="backing-up-azure-automation"></a>Tworzenie kopii zapasowych usługi Azure Automation
Podczas usuwania konta automatyzacji w systemie Microsoft Azure, wszystkie obiekty w koncie hello są usuwane, w tym elementów runbook, modułów, konfiguracji, ustawienia, zadania i zasoby. Nie można odzyskać Hello obiektów, po usunięciu konta hello.  Możesz użyć hello następujące informacje toobackup hello zawartość Twoje konto usługi Automatyzacja przed jego usunięciem. 

### <a name="runbooks"></a>Elementy Runbook
Możesz wyeksportować plików tooscript elementów runbook za pomocą portalu zarządzania Azure hello lub hello [Get-AzureAutomationRunbookDefinition](https://msdn.microsoft.com/library/dn690269.aspx) polecenia cmdlet programu Windows PowerShell.  Nie można zaimportować te pliki skryptów do innego konta automatyzacji, zgodnie z opisem w [Tworzenie lub importowanie elementu Runbook](https://msdn.microsoft.com/library/dn643637.aspx).

### <a name="integration-modules"></a>Moduły integracji
Moduły integracji nie można wyeksportować z usługi Automatyzacja Azure.  Pamiętaj, że są one dostępne poza hello konta automatyzacji.

### <a name="assets"></a>Elementy zawartości
Nie można wyeksportować [zasoby](https://msdn.microsoft.com/library/dn939988.aspx) usługi Automatyzacja Azure.  Przy użyciu hello portalu zarządzania Azure, należy zaznaczyć szczegóły hello zmienne, poświadczenia, certyfikatów, połączeń i harmonogramy.  Następnie należy ręcznie utworzyć wszelkie zasoby używane przez elementy runbook, importowany do innego automatyzacji.

Można użyć [poleceń cmdlet systemu Azure](https://msdn.microsoft.com/library/dn690262.aspx) tooretrieve szczegóły niezaszyfrowane zasoby i zapisać je w przyszłość odwołania lub utwórz zasoby równoważne na innym koncie automatyzacji.

Nie można pobrać wartości hello szyfrowane zmienne lub pole o hasła hello poświadczeń przy użyciu poleceń cmdlet.  Jeśli nie znasz tych wartości, a następnie można je pobrać od elementu runbook za pomocą hello [Get-AutomationVariable](https://msdn.microsoft.com/library/dn940012.aspx) i [Get-AutomationPSCredential](https://msdn.microsoft.com/library/dn940015.aspx) działań.

Nie można wyeksportować certyfikaty z usługi Automatyzacja Azure.  Pamiętaj, że wszystkie certyfikaty są dostępne poza platformą Azure.

### <a name="dsc-configurations"></a>Konfiguracji DSC
Możesz wyeksportować plików tooscript konfiguracje za pomocą portalu zarządzania Azure hello lub hello [AzureRmAutomationDscConfiguration eksportu](https://msdn.microsoft.com/library/mt603485.aspx) polecenia cmdlet programu Windows PowerShell. Te konfiguracje można zaimportować i użyć innego konta automatyzacji.

## <a name="geo-replication-in-azure-automation"></a>Replikacja geograficzna w automatyzacji Azure
Replikacja geograficzna, standardowego konta usługi Automatyzacja Azure wykonuje kopię zapasową konta danych tooa innego regionu geograficznego nadmiarowości. Regionu podstawowego można wybrać podczas konfigurowania konta, a następnie region pomocniczy jest przypisywana tooit automatycznie. dane dodatkowej Hello, skopiowane z hello regionu podstawowego, jest stale aktualizowany w przypadku utraty danych.  

Hello w poniższej tabeli przedstawiono hello par dostępne regionu podstawowego i pomocniczego.

| Podstawowy | Pomocniczy |
| --- | --- |
| Środkowo-południowe stany USA |Środkowo-północne stany USA |
| Wschodnie stany USA 2 |Środkowe stany USA |
| Europa Zachodnia |Europa Północna |
| Azja Południowo-Wschodnia |Azja Wschodnia |
| Japonia Wschodnia |Japonia Zachodnia |

W przypadku mało prawdopodobnego hello zgubienia danych regionu podstawowego, Microsoft podejmuje toorecover go. Jeśli nie można odzyskać danych podstawowych hello, pracy awaryjnej geograficzna jest wykonywane i hello użytkowników, których dotyczy zostanie poinformowany o to za pośrednictwem ich subskrypcji.

