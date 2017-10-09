---
title: "aaaStream hello dziennika aktywności platformy Azure tooEvent koncentratory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toostream hello tooEvent dziennika aktywności platformy Azure koncentratorów."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ec4c2d2c-8907-484f-a910-712403a06829
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/06/2017
ms.author: johnkem
ms.openlocfilehash: 336f92771b9d4379ad9dbcadc6997dfae7fae7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-hello-azure-activity-log-tooevent-hubs"></a>Strumienia tooEvent dziennika aktywności platformy Azure hello koncentratory
Witaj [ **dziennika aktywności platformy Azure** ](monitoring-overview-activity-logs.md) mogą być przesyłane strumieniowo w niemal w czasie rzeczywistym tooany aplikacji przy użyciu wbudowanych opcji "Eksportuj" hello, w portalu hello lub przez włączenie hello identyfikator reguły magistrali usług w profilu dziennika za pomocą hello Polecenia cmdlet programu PowerShell systemu Azure lub Azure CLI.

## <a name="what-you-can-do-with-hello-activity-log-and-event-hubs"></a>Co można zrobić z hello dziennika aktywności i usługi Event Hubs
Poniżej przedstawiono kilka sposobów może używać hello przesyłania strumieniowego dla hello dziennik aktywności możliwości:

* **Strumienia systemów firm toothird rejestrowania i dane telemetryczne** — wraz z upływem czasu przesyłania strumieniowego usługi Event Hubs ma zostać toopipe mechanizmu hello dziennik aktywności w innych rozwiązań Siem a dziennika rozwiązań analitycznych.
* **Tworzenie niestandardowych telemetrii i rejestrowanie platformy** — Jeśli masz już platformy telemetrii niestandardowej lub są po prostu pomyśleć o budynku jedną hello skalowalnej publikowania / subskrypcji rodzaj usługi Event Hubs umożliwia tooflexibly pozyskiwania hello Dziennik aktywności. [Zobacz Dan Rosanova przewodnik toousing centra zdarzeń w skali globalnej platformy telemetrii w tym miejscu.](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-hello-activity-log"></a>Przesyłania strumieniowego hello dziennik aktywności
Umożliwiają przesyłanie strumieniowe hello dziennik aktywności programowo lub za pośrednictwem portalu hello. W obu przypadkach wybierz Namespace magistrali usługi i zasady dostępu współdzielonego dla tej przestrzeni nazw i Centrum zdarzeń jest tworzony w tej przestrzeni nazw, po wystąpieniu zdarzenia dziennika aktywności nowe pierwszy hello. Jeśli nie masz Namespace magistrali usług, należy najpierw toocreate jeden. Jeśli wcześniej zostały strumieniowo toothis zdarzenia dziennika aktywności Namespace magistrali usług, hello Centrum zdarzeń, która została wcześniej utworzona zostanie ono użyte ponownie. zasady dostępu Hello udostępnionych definiuje hello uprawnienia hello mechanizm przesyłania strumieniowego. Obecnie wymaga przesyłania strumieniowego usługi Event Hubs tooan **Zarządzaj**, **wysyłania**, i **nasłuchiwania** uprawnienia. Można utworzyć lub zmodyfikować zasady dostępu Namespace magistrali usług udostępnionych w portalu klasycznym hello karcie "Konfiguruj" hello dla Twojego Namespace magistrali usługi. tooupdate hello dziennik aktywności dziennika profilu tooinclude przesyłania strumieniowego, użytkownik hello wprowadzeniu zmiany hello musi mieć uprawnienie ListKey hello w tej regule autoryzacji magistrali usługi.

Witaj bus lub event hub przestrzeni nazw usługi nie ma toobe w hello tej samej subskrypcji co subskrypcji hello emitowanie dzienniki tak długo, jak hello użytkownik, który konfiguruje ustawienia hello ma odpowiednie RBAC dostępu tooboth subskrypcji.

### <a name="via-azure-portal"></a>Za pomocą portalu Azure
1. Przejdź toohello **dziennik aktywności** przy użyciu hello menu na powitania po lewej stronie portalu hello bloku.
   
    ![Przejdź tooActivity dziennika w portalu](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. Kliknij przycisk hello **wyeksportować** u góry hello hello bloku.
   
    ![Przycisk Eksportuj w portalu](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. W wyświetlonym bloku hello można wybrać hello regionów, dla których chcesz toostream zdarzenia i hello usługi magistrali Namespace, w którym chcesz toobe Centrum zdarzeń utworzonych dla przesyłania strumieniowego te zdarzenia.
   
    ![Eksport dziennika aktywności bloku](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. Kliknij przycisk **zapisać** toosave te ustawienia. Ustawienia Hello są natychmiast być zastosowane tooyour subskrypcji.

### <a name="via-powershell-cmdlets"></a>Za pomocą poleceń cmdlet programu PowerShell
Jeśli istnieje już profil dziennika, należy najpierw tooremove tego profilu.

1. Użyj `Get-AzureRmLogProfile` tooidentify, jeśli istnieje już profil dziennika
2. Jeśli tak, użyj `Remove-AzureRmLogProfile` tooremove go.
3. Użyj `Set-AzureRmLogProfile` toocreate profil:

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

Hello identyfikator reguły magistrali usług to ciąg w formacie: {identyfikator zasobu magistrali usługi} /authorizationrules/ {nazwa klucza}, np. 

### <a name="via-azure-cli"></a>Za pomocą interfejsu wiersza polecenia platformy Azure
Jeśli istnieje już profil dziennika, należy najpierw tooremove tego profilu.

1. Użyj `azure insights logprofile list` tooidentify, jeśli istnieje już profil dziennika
2. Jeśli tak, użyj `azure insights logprofile delete` tooremove go.
3. Użyj `azure insights logprofile add` toocreate profil:

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

Hello identyfikator reguły magistrali usług to ciąg w formacie: `{service bus resource ID}/authorizationrules/{key name}`.

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>Jak korzystać z hello danych dziennika z usługi Event Hubs?
[Schemat Hello hello dziennik aktywności jest dostępnych tutaj](monitoring-overview-activity-logs.md). Każde wydarzenie jest w tablicy obiektów blob JSON o nazwie "rekordy."

## <a name="next-steps"></a>Następne kroki
* [Archiwum hello konta magazynu tooa dziennik aktywności](monitoring-archive-activity-log.md)
* [Omówienie hello odczytu hello dziennika aktywności platformy Azure](monitoring-overview-activity-logs.md)
* [Konfigurowanie alertu na podstawie zdarzenia dziennika aktywności](insights-auditlog-to-webhook-email.md)

