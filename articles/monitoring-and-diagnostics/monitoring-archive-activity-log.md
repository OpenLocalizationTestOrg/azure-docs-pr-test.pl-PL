---
title: "Witaj aaaArchive dziennika aktywności platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooarchive Azure aktywności logowania w celu przechowywania długoterminowego na koncie magazynu."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 58c6d3a3a31398287f66f76999d48f2942ab5109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="archive-hello-azure-activity-log"></a>Archiwum hello dziennika aktywności platformy Azure
W tym artykule zostanie przedstawiony sposób korzystania hello portalu Azure, poleceń cmdlet programu PowerShell lub interfejsu wiersza polecenia i Platform tooarchive Twojego [ **dziennika aktywności platformy Azure** ](monitoring-overview-activity-logs.md) na koncie magazynu. Ta opcja jest przydatna, jeśli chcesz tooretain dłużej niż 90 dni (z pełną kontrolę nad zasady przechowywania hello) dla dziennika aktywności inspekcji analizy statycznej lub kopii zapasowej. Jeśli potrzebujesz tylko tooretain zdarzeń przez 90 dni lub mniej można nie ma potrzeby tooset archiwizacji tooa konta magazynu, ponieważ zdarzenia dziennika aktywności są przechowywane w hello platformy Azure przez 90 dni bez włączania archiwizacji.

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem należy zbyt[Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich można archiwizować dziennik aktywności. Zdecydowanie zaleca się, że nie należy używać istniejącego konta magazynu z innych, niż monitorowania danych w niej przechowywane, dzięki czemu można lepiej kontrolować dostęp do danych toomonitoring. Jednak jeśli są również archiwizowanie dzienników diagnostycznych i konto magazynu tooa metryki, rozsądne może toouse znaczeniu konto magazynu działanie dziennika również tookeep wszystkie dane monitorowania w centralnej lokalizacji. Konto magazynu Hello, którego używasz, musi być konto magazynu ogólnego przeznaczenia, a nie konta magazynu obiektów blob. Witaj konta magazynu nie ma w hello toobe tej samej subskrypcji co subskrypcji hello emitowanie dzienniki tak długo, jak hello użytkownik, który konfiguruje ustawienia hello ma odpowiednie RBAC dostępu tooboth subskrypcji.

## <a name="log-profile"></a>Profil dziennika
hello tooarchive przy użyciu dowolnej z poniższych metod hello dziennik aktywności, ustaw hello **profilu dziennika** dla subskrypcji. Witaj dziennika profil definiuje typ hello zdarzeń, które są zapisywane lub przesyłane strumieniowo i hello dane wyjściowe — magazynu konta i/lub zdarzenia koncentratora. Definiuje również zasady przechowywania hello (liczba dni korzystania z tooretain) dla zdarzenia zapisane na koncie magazynu. Jeśli zasady przechowywania hello ustawiono toozero, zdarzenia są przechowywane w nieskończoność. W przeciwnym razie można go ustawić tooany wartość z zakresu od 1 do 2147483647. Zasady przechowywania są stosowane na dzień, więc na powitania koniec dnia (UTC), rejestruje od dnia hello, która jest teraz poza zasady przechowywania hello zostaną usunięte. Na przykład jeśli masz zasady przechowywania jeden dzień początku hello dzisiaj dzień hello hello dzienniki hello dzień przed wczoraj zostaną usunięte. [Więcej informacje dziennika tutaj profile](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile). 

## <a name="archive-hello-activity-log-using-hello-portal"></a>Dziennik aktywności za pomocą portalu hello hello archiwum
1. W portalu powitania kliknij hello **dziennik aktywności** łącze nawigacji po lewej stronie powitania. Jeśli nie widzisz łącze hello dziennik aktywności kliknij hello **więcej usług** najpierw łącza.
   
    ![Przejdź do bloku dziennika tooActivity](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. U góry hello hello bloku, kliknij przycisk **wyeksportować**.
   
    ![Kliknij przycisk Eksportuj hello](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. W wyświetlonym bloku hello Sprawdź pole hello **wyeksportować konta magazynu tooa** i wybierz konto magazynu.
   
    ![Ustaw konto magazynu](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. Za pomocą suwaka hello lub pola tekstowego, określić liczbę dni, dla których zdarzenia dziennika aktywności powinna być przechowywana w koncie magazynu. Jeśli wolisz toohave dane utrwalone na koncie magazynu hello nieskończoność, ustaw ten numer toozero.
5. Kliknij pozycję **Zapisz**.

## <a name="archive-hello-activity-log-via-powershell"></a>Archiwum hello dziennik aktywności za pomocą programu PowerShell
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| Właściwość | Wymagane | Opis |
| --- | --- | --- |
| StorageAccountId |Nie |Identyfikator zasobu hello konta magazynu toowhich Dzienniki aktywności ma zostać zapisany. |
| Lokalizacje |Tak |Rozdzielana przecinkami lista regionów, dla których chcesz toocollect dziennik zdarzeń. Można wyświetlić listę wszystkich regionach [, przechodząc na stronę tej strony](https://azure.microsoft.com/en-us/regions) lub za pomocą [hello interfejsu API REST zarządzania Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx). |
| retentionInDays |Tak |Liczba dni dla zdarzenia, które mają być przechowywane, od 1 do 2147483647. Wartość zero przechowuje dzienniki hello nieskończoność (zawsze). |
| Kategorie |Tak |Rozdzielana przecinkami lista kategorii zdarzeń, które powinny być zbierane. Możliwe wartości to zapisu, usuwania i akcji. |

## <a name="archive-hello-activity-log-via-cli"></a>Archiwum hello dziennik aktywności za pomocą interfejsu wiersza polecenia
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| Właściwość | Wymagane | Opis |
| --- | --- | --- |
| name |Tak |Nazwa profilu dziennika. |
| storageId |Nie |Identyfikator zasobu hello konta magazynu toowhich Dzienniki aktywności ma zostać zapisany. |
| Lokalizacje |Tak |Rozdzielana przecinkami lista regionów, dla których chcesz toocollect dziennik zdarzeń. Można wyświetlić listę wszystkich regionach [, przechodząc na stronę tej strony](https://azure.microsoft.com/en-us/regions) lub za pomocą [hello interfejsu API REST zarządzania Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx). |
| retentionInDays |Tak |Liczba dni dla zdarzenia, które mają być przechowywane, od 1 do 2147483647. Wartość zero będą przechowywane dzienniki hello nieskończoność (zawsze). |
| Kategorie |Tak |Rozdzielana przecinkami lista kategorii zdarzeń, które powinny być zbierane. Możliwe wartości to zapisu, usuwania i akcji. |

## <a name="storage-schema-of-hello-activity-log"></a>Schemat magazynu hello dziennik aktywności
Po skonfigurowaniu archiwizacji, kontenera magazynu zostanie utworzony na koncie magazynu hello zaraz po wystąpieniu zdarzenia dziennika aktywności. obiekty BLOB Hello w kontenerze hello wykonaj hello takiego samego formatu między hello dziennika aktywności i dzienników diagnostycznych. Struktura Hello tych obiektów blob jest:

> szczegółowe informacje operacyjne dzienniki/nazwa-= domyślne/resourceId = / SUBSKRYPCJI / {identyfikator subskrypcji} / y = {czterocyfrowy rok liczbowych} / m = {dwucyfrowe liczbowych month} / d = {dwucyfrowe liczbą dzień} / h = {dwucyfrowe 24-godzinnym hour}/m=00/PT1H.json
> 
> 

Na przykład może być nazwa obiektu blob:

> insights-Operational-Logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.JSON
> 
> 

Każdy obiekt blob PT1H.json zawiera obiektu blob JSON zdarzeń, które wystąpiły w ciągu godziny hello określona w adresie URL obiektu blob hello (np. h = 12). Podczas hello obecny godzinę zdarzenia są toohello dołączany plik PT1H.json miarę ich występowania. Witaj wartość minuty (m = 00) jest zawsze 00, ponieważ dziennik zdarzeń są podzielone na poszczególne obiekty BLOB na godzinę.

W pliku PT1H.json hello każde zdarzenie jest przechowywane w tablicy rekordy"hello", po tym formacie:

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
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
| category |Kategoria hello akcji, np. Zapis, Odczyt, akcji. |
| resultType |Witaj typu wyniku hello, np. Sukces, Niepowodzenie, Start |
| resultSignature |Zależy od typu zasobu hello. |
| durationMs |Czas trwania operacji hello w milisekundach |
| callerIpAddress |Adres IP hello użytkownik wykonał operację hello, oświadczenia UPN lub nazwy SPN oświadczenia na podstawie dostępności. |
| correlationId |Zazwyczaj identyfikator GUID w formacie ciągu hello. Zdarzenia, które mają correlationId należą toohello tę samą akcję pełny. |
| identity |Obiekt blob JSON opisujące hello autoryzacji i oświadczenia. |
| Autoryzacji |Obiekt typu blob właściwości RBAC hello zdarzenia. Obejmuje zazwyczaj hello właściwości "Akcja", "rola" i "zakresu". |
| poziom |Poziom hello zdarzeń. Jeden z hello następujące wartości: "Krytyczne", "Błąd", "Ostrzeżenie", "Informacyjny" i "Pełne" |
| location |Region, w którym miejscu hello wystąpił (lub globalne). |
| properties |Zestaw `<Key, Value>` pary (tj. Słownik) opisujący szczegóły hello hello zdarzenia. |

> [!NOTE]
> właściwości Hello i użycia tych właściwości zależy od zasobu hello.
> 
> 

## <a name="next-steps"></a>Następne kroki
* [Pobierać obiekty BLOB do analizy](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [Strumienia hello dziennik aktywności tooEvent koncentratory](monitoring-stream-activity-logs-event-hubs.md)
* [Więcej informacji na temat hello dziennik aktywności](monitoring-overview-activity-logs.md)

