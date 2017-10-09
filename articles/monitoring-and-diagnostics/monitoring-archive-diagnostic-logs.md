---
title: "aaaArchive dzienników diagnostycznych platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooarchive Twojego Diagnostyka Azure dzienników w celu przechowywania długoterminowego na koncie magazynu."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 3a55c73f-2ef3-45f3-8956-bcf9c0cb7e05
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: bc9edbd3a649023a728b7fe77130dba2b6e6370d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="archive-azure-diagnostic-logs"></a>Archiwum dzienników diagnostycznych platformy Azure
W tym artykule zostanie przedstawiony sposób hello portalu Azure, poleceń cmdlet programu PowerShell, interfejsu wiersza polecenia, użyj lub REST API tooarchive Twojego [Azure dzienników diagnostycznych](monitoring-overview-of-diagnostic-logs.md) na koncie magazynu. Ta opcja jest przydatna, jeśli chcesz tooretain dzienników diagnostyki sieci przy użyciu zasad przechowywania opcjonalne inspekcji, analizę statyczną lub kopii zapasowej. Witaj konta magazynu nie ma w hello toobe tej samej subskrypcji co zasób hello emitowanie dzienniki tak długo, jak hello użytkownik, który konfiguruje ustawienia hello ma odpowiednie RBAC dostępu tooboth subskrypcji.

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem należy zbyt[Utwórz konto magazynu](../storage/storage-create-storage-account.md) toowhich można archiwizować dzienników diagnostycznych. Zdecydowanie zaleca się, że nie należy używać istniejącego konta magazynu z innych, niż monitorowania danych w niej przechowywane, dzięki czemu można lepiej kontrolować dostęp do danych toomonitoring. Jednak jeśli są również Archiwizowanie dziennika aktywności, a konto magazynu diagnostyki metryki tooa, rozsądne może toouse znaczeniu tego konta magazynu dla Twojego dzienniki diagnostyczne również tookeep wszystkie dane monitorowania w centralnej lokalizacji. Konto magazynu Hello, którego używasz, musi być konto magazynu ogólnego przeznaczenia, a nie konta magazynu obiektów blob.

## <a name="diagnostic-settings"></a>Ustawienia diagnostyki
Ustaw tooarchive dzienników diagnostyki sieci przy użyciu dowolnej z poniższych metod hello, **ustawienie diagnostyczne** dla określonego zasobu. Ustawienie diagnostyczne dla zasobu definiuje hello kategorii dzienników i dane wysyłane tooa docelowego (konto magazynu, centra zdarzeń w przestrzeni nazw lub Log Analytics). Definiuje również zasady przechowywania hello (liczba dni korzystania z tooretain) dla zdarzenia każdej kategorii dziennika i dane przechowywane na koncie magazynu. Jeśli zasady przechowywania wynosi toozero, zdarzenia dla tej kategorii dziennika są przechowywane przez nieograniczony czas (to znaczy nieskończona toosay,). Zasady przechowywania, w przeciwnym razie może być dowolną liczbę dni od 1 do 2147483647. [Możesz przeczytać dodatkowe informacje w tym miejscu ustawień diagnostycznych](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings). Zasady przechowywania są stosowane na dzień, więc na powitania koniec dnia (UTC), rejestruje od dnia hello, która jest teraz poza zasady przechowywania hello zostaną usunięte. Na przykład jeśli masz zasady przechowywania jeden dzień początku hello dzisiaj dzień hello hello dzienniki hello dzień przed wczoraj zostaną usunięte

## <a name="archive-diagnostic-logs-using-hello-portal"></a>Dzienniki diagnostyczne archiwum przy użyciu portalu hello
1. W portalu hello Przejdź tooAzure monitora, a następnie kliknij **ustawień diagnostycznych**

    ![Monitorowanie sekcji Azure Monitor](media/monitoring-archive-diagnostic-logs/diagnostic-settings-blade.png)

2. Opcjonalnie Filtruj listę hello według grupy zasobów lub typ zasobu, a następnie kliknij na powitania zasobu, dla którego chcesz tooset ustawienie diagnostyczne.

3. Jeśli nie istnieją żadne ustawienia na powitania zasobów, wybrana przez Ciebie, jesteś toocreate zostanie wyświetlony monit o ustawienie. Kliknij pozycję "Włącz diagnostykę."

   ![Dodaj ustawienie diagnostyczne - żadnych istniejących ustawień](media/monitoring-archive-diagnostic-logs/diagnostic-settings-none.png)

   W przypadku ustawienia istniejące na powitania zasobów, zostanie wyświetlona lista ustawień już skonfigurowana dla tego zasobu. Kliknij przycisk "Dodaj ustawienie diagnostyczne".

   ![Dodaj ustawienie diagnostyczne — istniejące ustawienia](media/monitoring-archive-diagnostic-logs/diagnostic-settings-multiple.png)

3. Nadaj nazwę ustawienia i sprawdź pole hello **wyeksportować tooStorage konta**, wybierz konto magazynu. Opcjonalnie ustawić liczbę dni tooretain tych dzienników przy użyciu hello **przechowywania (dni)** suwaki. Przechowywanie zero dni przechowuje dzienniki hello nieskończoność.
   
   ![Dodaj ustawienie diagnostyczne — istniejące ustawienia](media/monitoring-archive-diagnostic-logs/diagnostic-settings-configure.png)
    
4. Kliknij pozycję **Zapisz**.

Po kilku chwilach hello nowe ustawienie jest wyświetlane na liście ustawień dla tego zasobu, a dzienników diagnostycznych są archiwizowane toothat magazynu konta zaraz po wygenerowaniu nowych danych zdarzenia.

## <a name="archive-diagnostic-logs-via-azure-powershell"></a>Dzienniki diagnostyczne archiwum za pomocą programu Azure PowerShell
```
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg -StorageAccountId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Categories networksecuritygroupevent,networksecuritygrouprulecounter -Enabled $true -RetentionEnabled $true -RetentionInDays 90
```

| Właściwość | Wymagane | Opis |
| --- | --- | --- |
| Identyfikator zasobu |Tak |Identyfikator zasobu hello zasobu, na którym tooset ustawienie diagnostyczne. |
| StorageAccountId |Nie |Identyfikator zasobu toowhich konta magazynu hello dzienników diagnostycznych ma zostać zapisany. |
| Kategorie |Nie |Rozdzielana przecinkami lista tooenable kategorie dziennika. |
| Enabled (Włączony) |Tak |Wartość logiczna wskazująca, czy diagnostycznych są włączone lub wyłączone w przypadku tego zasobu. |
| RetentionEnabled |Nie |Wartość logiczna wskazująca, czy zasady przechowywania są włączone dla tego zasobu. |
| retentionInDays |Nie |Liczba dni, dla których mają być przechowywane zdarzeń od 1 do 2147483647. Wartość zero przechowuje dzienniki hello nieskończoność. |

## <a name="archive-diagnostic-logs-via-hello-cross-platform-cli"></a>Dzienniki diagnostyczne archiwum za pośrednictwem hello interfejsu wiersza polecenia i Platform
```
azure insights diagnostic set --resourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg --storageId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage –categories networksecuritygroupevent,networksecuritygrouprulecounter --enabled true
```

| Właściwość | Wymagane | Opis |
| --- | --- | --- |
| resourceId |Tak |Identyfikator zasobu hello zasobu, na którym tooset ustawienie diagnostyczne. |
| storageId |Nie |Identyfikator zasobu hello dzienników diagnostycznych toowhich konto magazynu ma zostać zapisany. |
| Kategorie |Nie |Rozdzielana przecinkami lista tooenable kategorie dziennika. |
| włączone |Tak |Wartość logiczna wskazująca, czy diagnostycznych są włączone lub wyłączone w przypadku tego zasobu. |

## <a name="archive-diagnostic-logs-via-hello-rest-api"></a>Dzienniki diagnostyczne archiwum za pośrednictwem hello interfejsu API REST
[Zobacz ten dokument](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) informacji w sposób konfigurowania ustawienie diagnostyczne przy użyciu interfejsu API REST Monitor Azure hello.

## <a name="schema-of-diagnostic-logs-in-hello-storage-account"></a>Schemat dzienników diagnostycznych na koncie magazynu hello
Po skonfigurowaniu archiwizacji, kontenera magazynu jest tworzony na koncie magazynu hello zaraz po wystąpieniu zdarzenia w jednym z hello dziennika kategorie, które aktywowano. obiekty BLOB Hello w kontenerze hello wykonaj hello takiego samego formatu między dzienników diagnostycznych i hello dziennik aktywności. Struktura Hello tych obiektów blob jest:

> insights — dzienniki — {nazwa kategorii dziennika} / resourceId = / SUBSKRYPCJI / {identyfikator subskrypcji} /RESOURCEGROUPS/ {Nazwa grupy zasobów} /PROVIDERS/ {Nazwa dostawcy zasobów} / {typu zasobu} / {Nazwa zasobu} / y = {czterocyfrowy rok liczbowych} / m = {dwucyfrowe liczbowych month} / d = {dwucyfrowe liczbą dzień} / h = {dwucyfrowe 24-godzinnym hour}/m=00/PT1H.json
> 
> 

Lub po prostu,

> insights — dzienniki — {nazwa kategorii dziennika} / resourceId = / {identyfikator zasobu} / y = {czterocyfrowy rok liczbowych} / m = {dwucyfrowe liczbowych month} / d = {dwucyfrowe liczbą dzień} / h = {dwucyfrowe 24-godzinnym hour}/m=00/PT1H.json
> 
> 

Na przykład może być nazwa obiektu blob:

> insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json
> 
> 

Każdy obiekt blob PT1H.json zawiera obiektu blob JSON zdarzeń, które wystąpiły w ciągu godziny hello określona w adresie URL obiektu blob hello (na przykład h = 12). Podczas hello obecny godzinę zdarzenia są toohello dołączany plik PT1H.json miarę ich występowania. Witaj wartość minuty (m = 00) jest zawsze 00, ponieważ dziennik diagnostyczny zdarzenia są podzielone na poszczególne obiekty BLOB na godzinę.

W pliku PT1H.json hello każde zdarzenie jest przechowywane w tablicy rekordy"hello", po tym formacie:

```
{
    "records": [
        {
            "time": "2016-07-01T00:00:37.2040000Z",
            "systemId": "46cdbb41-cb9c-4f3d-a5b4-1d458d827ff1",
            "category": "NetworkSecurityGroupRuleCounter",
            "resourceId": "/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/TESTNSG",
            "operationName": "NetworkSecurityGroupCounters",
            "properties": {
                "vnetResourceGuid": "{12345678-9012-3456-7890-123456789012}",
                "subnetPrefix": "10.3.0.0/24",
                "macAddress": "000123456789",
                "ruleName": "/subscriptions/ s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg/securityRules/default-allow-rdp",
                "direction": "In",
                "type": "allow",
                "matchedConnections": 1988
            }
        }
    ]
}
```

| Nazwa elementu | Opis |
| --- | --- |
| time |Znacznik czasu w momencie hello zdarzeń został wygenerowany przez hello przetwarzania usługi Azure hello żądanie odpowiednie zdarzenie hello. |
| resourceId |Identyfikator zasobu hello wpływ na zasobów. |
| operationName |Nazwa operacji hello. |
| category |Kategoria dziennika zdarzeń hello. |
| properties |Zestaw `<Key, Value>` pary (tj. Słownik) opisujący szczegóły hello hello zdarzenia. |

> [!NOTE]
> właściwości Hello i użycia tych właściwości zależy od zasobu hello.
> 
> 

## <a name="next-steps"></a>Następne kroki
* [Pobierać obiekty BLOB do analizy](../storage/storage-dotnet-how-to-use-blobs.md)
* [Strumień diagnostycznych dzienników tooan centra zdarzeń w przestrzeni nazw](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Więcej informacji na temat dzienników diagnostycznych](monitoring-overview-of-diagnostic-logs.md)
