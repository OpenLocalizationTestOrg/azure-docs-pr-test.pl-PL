---
title: aaaAzure operacji dostawcy Resource Manager | Dokumentacja firmy Microsoft
description: "Szczegóły hello operacje dostępne dla dostawców zasobów hello Microsoft Azure Resource Manager"
services: active-directory
documentationcenter: 
author: jboeshart
manager: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: jaboes
ms.openlocfilehash: 2d2f912ecbade335667d68fdc42ce03a2930a0eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-resource-provider-operations"></a>Operacje Menedżera zasobów dostawcy zasobów platformy Azure

Ten dokument zawiera listę operacji hello dostępnych dla każdego dostawcy zasobów programu Microsoft Azure Resource Manager. Mogą być one używane w niestandardowych ról tooprovide szczegółowej kontroli dostępu opartej na rolach (RBAC) uprawnienia tooresources na platformie Azure. Należy pamiętać, nie jest to kompleksowe i operacje może dodać lub usunąć każdy dostawca jest aktualizowana. Operacja ciągów wykonaj hello format `Microsoft.<ProviderName>/<ChildResourceType>/<action>`. Lista bieżących i wszechstronne użyj `Get-AzureRmProviderOperation` (w programie PowerShell) lub `azure provider operations show` (w Azure CLI) operacji toolist dostawców zasobów platformy Azure.

## <a name="microsoftadhybridhealthservice"></a>Microsoft.ADHybridHealthService

| Operacja | Opis |
|---|---|
|/ configuration/działania|Aktualizacje konfiguracji dzierżawy.|
|/ services/działania|Aktualizacje w dzierżawie powitalnych wystąpienie usługi.|
|/ configuration/zapisu|Tworzy konfiguracji dzierżawy.|
|/Configuration/Read|Odczytuje hello konfiguracji dzierżawy.|
|/ services/zapisu|Tworzy wystąpienie usługi w dzierżawie powitalnych.|
|/Services/Read|Odczytuje wystąpień usługi hello w dzierżawie powitalnych.|
|/Services/DELETE|Usuwa wystąpienie usługi, w dzierżawie powitalnych.|
|/Services/servicemembers/Action|Tworzy wystąpienie elementu członkowskiego usługi w usłudze hello.|
|/Services/servicemembers/Read|Odczytuje wystąpienie elementu członkowskiego usługi hello hello usługi.|
|/Services/servicemembers/DELETE|Usuwa wystąpienie elementu członkowskiego usługi w usłudze hello.|
|/Services/servicemembers/Alerts/Read|Odczytuje hello alerty dla elementu członkowskiego usługi.|
|/Services/Alerts/Read|Odczytuje hello alerty dla usługi.|
|/Services/Alerts/Read|Odczytuje hello alerty dla usługi.|

## <a name="microsoftadvisor"></a>Microsoft.Advisor

| Operacja | Opis |
|---|---|
|/ generateRecommendations/działania|Generuje zalecenia|
|/ pominięć/działania|Tworzy aktualizacje pominięć|
|/ register/działania|Rejestruje subskrypcję hello hello Advisor firmy Microsoft|
|/generateRecommendations/Read|Pobiera Generowanie zaleceń stanu|
|/recommendations/Read|Odczytuje zalecenia|
|/suppressions/Read|Pobiera pominięć|
|/suppressions/DELETE|Usuwa pominięć|

## <a name="microsoftanalysisservices"></a>Microsoft.AnalysisServices

| Operacja | Opis |
|---|---|
|/Servers/Read|Pobiera informacje hello hello określony Analysis Server.|
|/ serwery/zapisu|Tworzy lub aktualizuje hello określony Analysis Server.|
|/Servers/DELETE|Usuwa hello Analysis Server.|
|/Servers/suspend/Action|Wstrzymuje hello Analysis Server.|
|/Servers/resume/Action|Wznawia hello Analysis Server.|
|/ serwery/checkNameAvailability<br>Action|Sprawdza, czy dany serwer analiz nazwa jest prawidłowa, a nie korzystać.|

## <a name="microsoftapimanagement"></a>Microsoft.ApiManagement

| Operacja | Opis |
|---|---|
|/ checkNameAvailability/działania|Sprawdza, czy pod warunkiem, że nazwa usługi jest niedostępna|
|/ register/działania|Zarejestruj subskrypcję dostawcy zasobów Microsoft.ApiManagement|
|/ unregister/działania|Wyrejestrowanie subskrypcji dla dostawcy zasobów Microsoft.ApiManagement|
|/ service/zapisu|Utwórz nowe wystąpienie interfejsu API usługi zarządzania|
|/Service/Read|Odczytać metadanych dla wystąpienia interfejsu API usługi zarządzania|
|/Service/DELETE|Usuń wystąpienia usługi interfejsu API zarządzania|
|/Service/updatehostname/Action|Konfiguracja, zaktualizować lub usunąć nazwy domeny niestandardowej dla usługi interfejsu API zarządzania|
|/Service/uploadcertificate/Action|Przekaż certyfikat protokołu SSL dla interfejsu API usługi zarządzania|
|/Service/Backup/Action|Kopia zapasowa usługi interfejsu API zarządzania toohello określonego kontenera użytkownika podane konto magazynu|
|/Service/Restore/Action|Przywracanie usługi interfejsu API zarządzania z określonego kontenera hello użytkownika podane konto magazynu|
|/Service/managedeployments/Action|Zmień jednostki SKU/jednostki, dodawania i usuwania wdrożenia regionalnych interfejsu API usługi zarządzania|
|/Service/getssotoken/Action|Pobiera token logowania jednokrotnego, które mogą być używane toologin do interfejsu API zarządzania usługi starszych portalu jako administrator|
|/Service/applynetworkconfigurationupdates/Action|Zasoby Microsoft.ApiManagement hello aktualizacji w sieci wirtualnej toopick zaktualizować ustawienia sieciowe.|
|/Service/operationresults/Read|Pobiera bieżący stan długotrwałej operacji|
|/Service/networkStatus/Read|Pobiera stan dostępu do sieci hello zasobów.|
|/Service/loggers/Read|Pobierz listę rejestratorów lub pobrać szczegółów rejestratora|
|/Service/loggers/Write|Dodać nowego rejestratora lub zaktualizować istniejący szczegóły rejestratora|
|/Service/loggers/DELETE|Usuń istniejące rejestratora|
|/Service/Users/Read|Pobierz listę zarejestrowanych użytkowników lub pobrać szczegółów konta użytkownika|
|/Service/Users/Write|Zarejestrować nowego użytkownika lub szczegóły konta aktualizacji istniejącego użytkownika|
|/Service/Users/DELETE|Usuwanie konta użytkownika|
|/Service/Users/generateSsoUrl/Action|Generowania adresu URL logowania jednokrotnego. adres URL Hello może być używane tooaccess portalu administratora|
|/Service/Users/Subscriptions/Read|Pobierz listę subskrypcji użytkownika|
|/Service/Users/keys/Read|Pobierz listę kluczy użytkownika|
|/Service/Users/groups/Read|Pobierz listę grup użytkowników|
|/Service/tenant/operationResults/Read|Pobierz listę wyników operacji lub uzyskanie wyniku operacji|
|/Service/tenant/Policy/Read|Uzyskiwanie konfiguracji zasad dla dzierżawcy hello|
|/Service/tenant/Policy/Write|Ustaw konfigurację zasad dla dzierżawy hello|
|/Service/tenant/Policy/DELETE|Usuń konfigurację zasad hello dzierżawy|
|/Service/tenant/Configuration/Save/Action|Tworzy zatwierdzenia z konfiguracji migawki toohello określonej gałęzi w repozytorium hello|
|/Service/tenant/Configuration/Deploy/Action|Uruchamia zadanie wdrażania zmian tooapply z hello git określonej gałęzi toohello konfiguracji w bazie danych.|
|/Service/tenant/Configuration/Validate/Action|Weryfikuje zmian z gałęzi git określonego hello|
|/Service/tenant/Configuration/operationResults/Read|Pobierz listę wyników operacji lub uzyskanie wyniku operacji|
|/Service/tenant/Configuration/syncState/Read|Pobierz stan ostatniej synchronizacji git|
|/Service/tenant/Access/Read|Uzyskaj dostęp do dzierżawy szczegółowe informacje o|
|/Service/tenant/Access/Write|Szczegółowe informacje dotyczące dzierżawy dostępu do informacji o aktualizacji|
|/Service/tenant/Access/regeneratePrimaryKey/Action|Ponownie wygenerować podstawowy klucz dostępu|
|/Service/tenant/Access/regenerateSecondaryKey/Action|Wygeneruj ponownie pomocniczy klucz dostępu|
|/Service/identityProviders/Read|Pobierz listę dostawców tożsamości lub Uzyskaj szczegóły dostawcy tożsamości|
|/Service/identityProviders/Write|Utwórz nowe szczegóły dostawcy tożsamości lub aktualizację istniejącego dostawcy tożsamości|
|/Service/identityProviders/DELETE|Usuń istniejące dostawcy tożsamości|
|/Service/Subscriptions/Read|Pobiera listę subskrypcji produktu lub uzyskać szczegółów subskrypcji produktu|
|/Service/Subscriptions/Write|Subskrypcja istniejącego użytkownika tooan istniejącego produktu lub zaktualizować istniejący Szczegóły subskrypcji. Ta operacja może być używane toorenew subskrypcji|
|/Service/Subscriptions/DELETE|Usuń subskrypcję. Ta operacja może być używane toodelete subskrypcji|
|/Service/Subscriptions/regeneratePrimaryKey/Action|Ponowne generowanie klucza podstawowego subskrypcji|
|/Service/Subscriptions/regenerateSecondaryKey/Action|Ponowne wygenerowanie klucza pomocniczego subskrypcji|
|/Service/backends/Read|Pobierz listę zapleczy lub uzyskać szczegółowe informacje o wewnętrznej bazy danych|
|/Service/backends/Write|Dodać nowego zaplecza lub zaktualizować istniejący szczegóły wewnętrznej bazy danych|
|/Service/backends/DELETE|Usuń istniejące wewnętrznej bazy danych|
|/Service/APIs/Read|Pobierz listę wszystkich zarejestrowanych szczegółów interfejsów API lub Get interfejsu API|
|/Service/APIs/Write|Utwórz nowy interfejs API lub zaktualizuj istniejącą szczegóły interfejsu API|
|/Service/APIs/DELETE|Usuń istniejące interfejsu API|
|/Service/APIs/Policy/Read|Uzyskiwanie szczegółów konfiguracji zasad interfejsu API|
|/Service/APIs/Policy/Write|Ustaw szczegóły konfiguracji zasad interfejsu API|
|/Service/APIs/Policy/DELETE|Usuń konfigurację zasad z interfejsu API|
|/Service/APIs/Operations/Read|Pobierz listę istniejących operacji interfejsu API lub uzyskać szczegółowe informacje o operacji interfejsu API|
|/Service/APIs/Operations/Write|Tworzenie nowej operacji interfejsu API lub zaktualizować istniejący operacji interfejsu API|
|/Service/APIs/Operations/DELETE|Usuń istniejące operacji interfejsu API|
|/Service/APIs/Operations/Policy/Read|Uzyskiwanie szczegółów konfiguracji zasad dla operacji|
|/Service/APIs/Operations/Policy/Write|Ustaw szczegóły konfiguracji zasad dla operacji|
|/Service/APIs/Operations/Policy/DELETE|Usuń konfigurację zasad z operacji|
|/Service/Products/Read|Pobierz listę produktów lub uzyskać szczegółowe informacje o produkcie|
|/Service/Products/Write|Tworzenie nowego produktu lub zaktualizować istniejące informacje szczegółowe|
|/Service/Products/DELETE|Usuń istniejące produkt|
|/Service/Products/Subscriptions/Read|Pobierz listę subskrypcji produktu|
|/Service/Products/APIs/Read|Pobierz listę produktów tooexisting dodano interfejsy API|
|/Service/Products/APIs/Write|Dodaj istniejący produkt tooexisting interfejsu API|
|/Service/Products/APIs/DELETE|Usuń istniejące interfejsu API z istniejącego produktu|
|/Service/Products/Policy/Read|Uzyskiwanie konfiguracji zasad istniejącego produktu|
|/Service/Products/Policy/Write|Ustaw konfigurację zasad dla istniejącego produktu|
|/Service/Products/Policy/DELETE|Usuń zasady konfiguracji z istniejącego produktu|
|/Service/Products/groups/Read|Pobierz listę grup developer skojarzonych z produktu|
|/Service/Products/groups/Write|Skojarz istniejąca grupa deweloperów z istniejącego produktu|
|/Service/Products/groups/DELETE|Usuń skojarzenie istniejąca grupa deweloperów z istniejącego produktu|
|/Service/openidConnectProviders/Read|Pobierz listę dostawców OpenID Connect lub pobranie szczegółów OpenID Connect dostawcy|
|/Service/openidConnectProviders/Write|Utwórz nowe szczegóły OpenID Connect dostawcy lub aktualizację istniejącego dostawcy uwierzytelniania OpenID Connect|
|/Service/openidConnectProviders/DELETE|Usuń istniejące OpenID Connect dostawcy|
|/Service/Certificates/Read|Pobierz listę certyfikatów lub Pobierz szczegóły certyfikatu|
|/Service/Certificates/Write|Dodaj nowy certyfikat|
|/Service/Certificates/DELETE|Usuń istniejący certyfikat|
|/Service/Properties/Read|Pobiera listę właściwości wszystkich lub pobiera szczegóły określonej właściwości|
|/Service/Properties/Write|Tworzy nową właściwość lub aktualizuje wartość dla określonej właściwości|
|/Service/Properties/DELETE|Usuwa istniejące właściwości|
|/Service/groups/Read|Pobierz listę grup lub pobiera szczegóły grupy|
|/Service/groups/Write|Utwórz nową grupę lub zaktualizować istniejący szczegóły grupy|
|/Service/groups/DELETE|Usuń istniejącą grupę|
|/Service/groups/Users/Read|Pobierz listę grupy użytkowników|
|/Service/groups/Users/Write|Dodaj istniejącą grupę tooexisting użytkowników|
|/Service/groups/Users/DELETE|Usuwanie istniejącego użytkownika z istniejącej grupy|
|/Service/authorizationServers/Read|Pobierz listę serwerów autoryzacji lub pobrać szczegółów serwera autoryzacji|
|/Service/authorizationServers/Write|Tworzenie nowego serwera autoryzacji lub szczegóły aktualizacji istniejącego serwera autoryzacji|
|/Service/authorizationServers/DELETE|Usuń istniejący serwer autoryzacji|
|/Service/Reports/bySubscription/Read|Pobierz raportu w subskrypcji.|
|/Service/Reports/byRequest/Read|Pobrać żądań danych raportowania|
|/Service/Reports/byOperation/Read|Raport w operacji|
|/Service/Reports/byGeo/Read|Raport w regionie geograficznym|
|/Service/Reports/byUser/Read|Pobierz raport agregowana przez deweloperów.|
|/Service/Reports/byTime/Read|Raport w okresach czasu|
|/Service/Reports/byApi/Read|Raport agregowana przez interfejsy API|
|/Service/Reports/byProduct/Read|Pobierz raport w produktów.|

## <a name="microsoftappservice"></a>Microsoft.AppService

| Operacja | Opis |
|---|---|
|/ appidentities/odczytu|Zwraca hello zasobów (witryny sieci web) w zarejestrowany hello bramy.|
|/ appidentities/zapisu|Tworzy nową tożsamość aplikacji.|
|/ appidentities/Delete|Usuwa istniejącą tożsamość aplikacji.|
|/deploymenttemplates/listMetadata/Action|Wyświetla listę metadanych interfejsu użytkownika powiązanych z hello pakiet aplikacji interfejsu API.|
|/deploymenttemplates/Generate/Action|Zwraca tooprovision Szablon wdrożenia wystąpienia aplikacji interfejsu API.|
|/ bram/odczytu|Zwraca hello wystąpienia bramy.|
|/ bram/zapisu|Tworzy nową bramę lub aktualizuje istniejący.|
|/ bram/Delete|Usuwa istniejące wystąpienie bramy.|
|/Gateways/listLoginUris/Action|Wypełnia magazynu tokenów i zwraca logowania OAuth identyfikatorów URI.|
|/Gateways/listKeys/Action|Zwraca klucze tajne bramy.|
|/Gateways/tokens/Write|Tworzy nowy Zumo Token o hello podanej nazwie.|
|/Gateways/Registrations/Read|Zwraca hello zasobów (witryny sieci web) w zarejestrowany hello bramy.|
|/Gateways/Registrations/Write|Rejestruje hello bramy zasobów (witryny sieci web).|
|/Gateways/Registrations/DELETE|Wyrejestrowuje zasobu (witryny sieci web) z hello bramy.|
|/ apiapps/odczytu|Zwraca hello wystąpieniu aplikacji interfejsu API.|
|/ apiapps/zapisu|Tworzy nową aplikację interfejsu API lub aktualizuje istniejący.|
|/ apiapps/Delete|Usuwa istniejące wystąpienie aplikacji interfejsu API.|
|/apiapps/listStatus/Action|Zwraca stan aplikacji interfejsu API.|
|/apiapps/listKeys/Action|Zwraca klucze tajne aplikacji interfejsu API.|
|/apiapps/apidefinitions/Read|Zwraca definicji interfejsu API aplikacji interfejsu API.|

## <a name="microsoftauthorization"></a>Microsoft.Authorization

| Operacja | Opis |
|---|---|
|/ elevateAccess/działania|Przyznaje hello wywołującego dostępu Administrator dostępu użytkowników w zakresie dzierżawy hello|
|/classicAdministrators/Read|Odczytuje Administratorzy hello hello subskrypcji.|
|/ classicAdministrators/zapisu|Dodaje lub modyfikuje administratora tooa subskrypcji.|
|/classicAdministrators/DELETE|Usuwa hello administratora z subskrypcji hello.|
|/Locks/Read|Pobiera blokady w hello określony zakres.|
|/ blokady zapisu|Dodaje blokady w hello określony zakres.|
|/Locks/DELETE|Usuwanie blokady w hello określony zakres.|
|/policyAssignments/Read|Pobierz informacje o przypisaniu zasad.|
|/ policyAssignments/zapisu|Tworzenie zasad przydziału na powitania określony zakres.|
|/policyAssignments/DELETE|Usuń przypisanie zasad w hello określony zakres.|
|/permissions/Read|Wyświetla wszystkie hello uprawnienia hello wywołującego w danym zakresie.|
|/roleDefinitions/Read|Pobiera informacje o definicji roli.|
|/ roleDefinitions/zapisu|Tworzy lub aktualizuje niestandardową definicję roli z określonymi uprawnieniami i zakresami możliwymi do przypisania.|
|/roleDefinitions/DELETE|Usuń hello określić niestandardową definicję roli.|
|/providerOperations/Read|Pobiera operacje dla wszystkich dostawców zasobów do użycia w definicjach ról.|
|/policyDefinitions/Read|Pobierz informacje o definicji zasad.|
|/ policyDefinitions/zapisu|Utwórz definicję zasad niestandardowych.|
|/policyDefinitions/DELETE|Usuń definicję zasad.|
|/roleAssignments/Read|Pobiera informacje o przypisaniu roli.|
|/ roleAssignments/zapisu|Tworzenie roli przydziału na powitania określony zakres.|
|/roleAssignments/DELETE|Usuń przypisanie roli w hello określony zakres.|

## <a name="microsoftautomation"></a>Microsoft.Automation

| Operacja | Opis |
|---|---|
|/automationAccounts/Read|Pobiera konto usługi Automatyzacja Azure|
|/ automationAccounts/zapisu|Tworzy lub aktualizuje konto usługi Automatyzacja Azure|
|/automationAccounts/DELETE|Usuwa konto usługi Automatyzacja Azure|
|/automationAccounts/Configurations/readContent/Action|Pobiera zawartość DSC automatyzacji Azure|
|/automationAccounts/hybridRunbookWorkerGroups/Read|Odczytuje zasoby hybrydowego procesu roboczego elementu Runbook|
|/automationAccounts/hybridRunbookWorkerGroups/DELETE|Usuwa zasoby hybrydowego procesu roboczego elementu Runbook|
|/automationAccounts/jobSchedules/Read|Pobiera harmonogram zadań usługi Automatyzacja Azure|
|/automationAccounts/jobSchedules/Write|Tworzy harmonogram zadań usługi Automatyzacja Azure|
|/automationAccounts/jobSchedules/DELETE|Usuwa harmonogram zadań usługi Automatyzacja Azure|
|/automationAccounts/connectionTypes/Read|Pobiera zasób typu połączenia usługi Automatyzacja Azure|
|/automationAccounts/connectionTypes/Write|Tworzy zasób typu połączenia usługi Automatyzacja Azure|
|/automationAccounts/connectionTypes/DELETE|Usuwa zasób typu połączenia usługi Automatyzacja Azure|
|/automationAccounts/Modules/Read|Pobiera moduł usługi Automatyzacja Azure|
|/automationAccounts/Modules/Write|Tworzy lub aktualizuje moduł usługi Automatyzacja Azure|
|/automationAccounts/Modules/DELETE|Usuwa moduł usługi Automatyzacja Azure|
|/automationAccounts/Credentials/Read|Pobiera zasób poświadczenia usługi Automatyzacja Azure|
|/automationAccounts/Credentials/Write|Tworzy lub aktualizuje zasób poświadczenia usługi Automatyzacja Azure|
|/automationAccounts/Credentials/DELETE|Usuwa zasób poświadczenia usługi Automatyzacja Azure|
|/automationAccounts/Certificates/Read|Pobiera zasób certyfikatu usługi Automatyzacja Azure|
|/automationAccounts/Certificates/Write|Tworzy lub aktualizuje zasób certyfikatu usługi Automatyzacja Azure|
|/automationAccounts/Certificates/DELETE|Usuwa zasób certyfikatu usługi Automatyzacja Azure|
|/automationAccounts/Schedules/Read|Pobiera zasób harmonogramu usługi Automatyzacja Azure|
|/automationAccounts/Schedules/Write|Tworzy lub aktualizuje zasób harmonogramu usługi Automatyzacja Azure|
|/automationAccounts/Schedules/DELETE|Usuwa zasób harmonogramu usługi Automatyzacja Azure|
|/automationAccounts/Jobs/Read|Pobiera zadanie usługi Automatyzacja Azure|
|/automationAccounts/Jobs/Write|Tworzy zadanie usługi Automatyzacja Azure|
|/automationAccounts/Jobs/Stop/Action|Zatrzymuje zadanie usługi Automatyzacja Azure|
|/automationAccounts/Jobs/suspend/Action|Wstrzymuje zadanie usługi Automatyzacja Azure|
|/automationAccounts/Jobs/resume/Action|Wznawia zadanie usługi Automatyzacja Azure|
|/automationAccounts/Jobs/runbookContent/Action|Pobiera hello zawartość elementu runbook usługi Automatyzacja Azure hello w czasie wykonywania zadania hello hello|
|/automationAccounts/Jobs/Output/Action|Pobiera hello dane wyjściowe zadania|
|/automationAccounts/Jobs/Read|Pobiera zadanie usługi Automatyzacja Azure|
|/automationAccounts/Jobs/Write|Tworzy zadanie usługi Automatyzacja Azure|
|/automationAccounts/Jobs/Stop/Action|Zatrzymuje zadanie usługi Automatyzacja Azure|
|/automationAccounts/Jobs/suspend/Action|Wstrzymuje zadanie usługi Automatyzacja Azure|
|/automationAccounts/Jobs/resume/Action|Wznawia zadanie usługi Automatyzacja Azure|
|/automationAccounts/Jobs/streams/Read|Pobiera strumień zadań usługi Automatyzacja Azure|
|/automationAccounts/Connections/Read|Pobiera zasób połączenia usługi Automatyzacja Azure|
|/automationAccounts/Connections/Write|Tworzy lub aktualizuje zasób połączenia usługi Automatyzacja Azure|
|/automationAccounts/Connections/DELETE|Usuwa zasób połączenia usługi Automatyzacja Azure|
|/automationAccounts/variables/Read|Odczytuje zasób zmiennej usługi Automatyzacja Azure|
|/automationAccounts/variables/Write|Tworzy lub aktualizuje zasób zmiennej usługi Automatyzacja Azure|
|/automationAccounts/variables/DELETE|Usuwa zasób zmiennej usługi Automatyzacja Azure|
|/automationAccounts/runbooks/readContent/Action|Pobiera hello zawartość elementu runbook usługi Automatyzacja Azure|
|/automationAccounts/runbooks/Read|Pobiera element runbook usługi Automatyzacja Azure|
|/automationAccounts/runbooks/Write|Tworzy lub aktualizuje element runbook usługi Automatyzacja Azure|
|/automationAccounts/runbooks/DELETE|Usuwa element runbook usługi Automatyzacja Azure|
|/automationAccounts/runbooks/draft/readContent/Action|Pobiera hello zawartość wersji roboczej elementu runbook usługi Automatyzacja Azure|
|/automationAccounts/runbooks/draft/writeContent/Action|Tworzy hello zawartość wersji roboczej elementu runbook usługi Automatyzacja Azure|
|/automationAccounts/runbooks/draft/Read|Pobiera wersję roboczą elementu runbook usługi Automatyzacja Azure|
|/automationAccounts/runbooks/draft/publish/Action|Publikuje wersję roboczą elementu runbook usługi Automatyzacja Azure|
|/automationAccounts/runbooks/draft/undoEdit/Action|Cofnij edycję wersji roboczej elementu runbook usługi Automatyzacja Azure dla tooan|
|/automationAccounts/runbooks/draft/testJob/Read|Pobiera zadanie testowe wersji roboczej elementu runbook usługi Automatyzacja Azure|
|/automationAccounts/runbooks/draft/testJob/Write|Tworzy zadanie testowe wersji roboczej elementu runbook usługi Automatyzacja Azure|
|/automationAccounts/runbooks/draft/testJob/Stop/Action|Zatrzymuje zadanie testowe wersji roboczej elementu runbook usługi Automatyzacja Azure|
|/automationAccounts/runbooks/draft/testJob/suspend/Action|Wstrzymuje zadanie testowe wersji roboczej elementu runbook usługi Automatyzacja Azure|
|/automationAccounts/runbooks/draft/testJob/resume/Action|Wznawia zadanie testowe wersji roboczej elementu runbook usługi Automatyzacja Azure|
|/automationAccounts/webhooks/Read|Odczytuje element webhook usługi Automatyzacja Azure|
|/automationAccounts/webhooks/Write|Tworzy lub aktualizuje element webhook usługi Automatyzacja Azure|
|/automationAccounts/webhooks/DELETE|Usuwa element webhook usługi Automatyzacja Azure |
|/automationAccounts/webhooks/generateUri/Action|Generuje identyfikator URI dla elementu webhook usługi Automatyzacja Azure|

## <a name="microsoftazureactivedirectory"></a>Microsoft.AzureActiveDirectory

Ten dostawca nie jest pełną dostawcy ARM i nie zapewnia żadnych operacji ARM.

## <a name="microsoftbatch"></a>Microsoft.Batch

| Operacja | Opis |
|---|---|
|/ register/działania|Rejestruje subskrypcję hello hello dostawcy zasobów partii i umożliwia hello tworzenia kont usługi partia zadań|
|/ batchAccounts/zapisu|Tworzy nowe konto wsadowe lub aktualizuje istniejące konto usługi partia zadań|
|/batchAccounts/Read|Lista kont usługi partia zadań lub pobiera właściwości hello konta usługi partia zadań|
|/batchAccounts/DELETE|Usuwa konto usługi partia zadań|
|/batchAccounts/listkeys/Action|Wyświetla uzyskać dostęp do kluczy dla konta usługi partia zadań|
|/batchAccounts/regeneratekeys/Action|Odtwarza uzyskać dostęp do kluczy dla konta usługi partia zadań|
|/batchAccounts/syncAutoStorageKeys/Action|Synchronizuje klucze dostępu dla konta magazynu automatycznie hello skonfigurowanych dla konta usługi partia zadań|
|/batchAccounts/Applications/Read|Wyświetla listę aplikacji lub pobiera właściwości hello aplikacji|
|/batchAccounts/Applications/Write|Tworzy nową aplikację lub aktualizuje istniejącą aplikację|
|/batchAccounts/Applications/DELETE|Usuwa aplikacji|
|/batchAccounts/Applications/Versions/Read|Pobiera właściwości hello pakietu aplikacji|
|/batchAccounts/Applications/Versions/Write|Tworzy nowy pakiet aplikacji lub aktualizuje istniejący pakiet aplikacji|
|/batchAccounts/Applications/Versions/Activate/Action|Aktywuje pakietu aplikacji|
|/batchAccounts/Applications/Versions/DELETE|Usuwa pakiet aplikacji|
|/Locations/Quotas/Read|Pobiera partii przydziały hello określonej subskrypcji w wybranym regionie Azure hello|

## <a name="microsoftbilling"></a>Microsoft.Billing

| Operacja | Opis |
|---|---|
|/Invoices/Read|Wyświetla dostępne faktury|

## <a name="microsoftbingmaps"></a>Microsoft.BingMaps

| Operacja | Opis |
|---|---|
|/ mapApis/odczytu|Operacja odczytu|
|/ mapApis/zapisu|Operacja zapisu|
|/ mapApis/Delete|Operacja usuwania|
|/mapApis/regenerateKey/Action|Generuje ponownie hello klucza|
|/mapApis/listSecrets/Action|Witaj listy kluczy tajnych|
|/mapApis/listSingleSignOnToken/Action|Witaj odczytu pojedynczy znak na autoryzacji tokenu dla zasobów|
|Operacje/odczytu|Opis operacji hello.|

## <a name="microsoftcache"></a>Microsoft.Cache

| Operacja | Opis |
|---|---|
|/ checknameavailability/działania|Sprawdza, czy nazwa jest dostępna do użycia z nowej pamięci podręcznej Redis|
|/ register/działania|Rejestruje subskrypcję dostawcy zasobów "Microsoft.Cache" hello|
|/ unregister/działania|Wyrejestrowuje dostawca zasobów "Microsoft.Cache" hello, z subskrypcją|
|/ redis/zapisu|Zmodyfikuj ustawienia i konfigurację w portalu zarządzania hello hello pamięci podręcznej Redis|
|/redis/Read|Wyświetl ustawienia i konfigurację hello pamięci podręcznej Redis w portalu zarządzania hello|
|/redis/DELETE|Usuń hello całą pamięć podręczną Redis|
|/redis/listKeys/Action|Widok hello wartość kluczy dostępu pamięci podręcznej Redis w portalu zarządzania hello|
|/redis/regenerateKey/Action|Zmień wartość hello kluczy dostępu pamięci podręcznej Redis w portalu zarządzania hello|
|/redis/Import/Action|Zaimportuj dane w podanym formacie z wielu obiektów blob do usługi Redis|
|/redis/Export/Action|Eksportowanie obiektów blob magazynu tooprefixed danych Redis w określonym formacie|
|/redis/forceReboot/Action|Wymuś ponowny rozruch wystąpienia pamięci podręcznej, nawet z utratą danych.|
|/redis/Stop/Action|Zatrzymanie wystąpienia pamięci podręcznej.|
|/redis/Start/Action|Uruchom wystąpienie pamięci podręcznej.|
|/redis/metricDefinitions/Read|Pobiera hello dostępne metryki pamięci podręcznej Redis|
|/redis/firewallRules/Read|Pobieranie reguł zapory IP hello pamięci podręcznej Redis|
|/redis/firewallRules/Write|Edytowanie reguły zapory IP hello pamięci podręcznej Redis|
|/redis/firewallRules/DELETE|Usuwanie reguły zapory IP pamięci podręcznej Redis|
|/redis/listUpgradeNotifications/Read|Lista hello najnowszych powiadomień o uaktualnieniach dla dzierżawy pamięci podręcznej hello.|
|/redis/linkedservers/Read|Pobierz połączone serwery skojarzone z pamięci podręcznej redis.|
|/redis/linkedservers/Write|Dodaj tooa połączonego serwera pamięci podręcznej Redis|
|/redis/linkedservers/DELETE|Usuń serwer połączony z pamięci podręcznej Redis|
|/redis/patchSchedules/Read|Pobiera hello stosowanie poprawek harmonogram pamięci podręcznej Redis|
|/redis/patchSchedules/Write|Modyfikowanie hello poprawki harmonogram pamięci podręcznej Redis|
|/redis/patchSchedules/DELETE|Usuń harmonogram poprawki hello pamięci podręcznej Redis|

## <a name="microsoftcertificateregistration"></a>Microsoft.CertificateRegistration

| Operacja | Opis |
|---|---|
|/ provisionGlobalAppServicePrincipalInUserTenant/działania|Zainicjuj obsługę nazwy głównej usługi dla nazwy głównej usługi aplikacji|
|/ validateCertificateRegistrationInformation/działania|Sprawdzanie poprawności obiektu zakupu certyfikatu bez przesyłania|
|/ register/działania|Rejestrowanie dostawcy zasobów Certificates Microsoft hello hello subskrypcji|
|/ certificateOrders/zapisu|Dodaj nowy certificateOrder lub zaktualizuj istniejącą|
|/ certificateOrders/Delete|Usuń istniejące AppServiceCertificate|
|/ certificateOrders/odczytu|Pobierz listę hello CertificateOrders|
|/certificateOrders/reissue/Action|Wydaj ponownie istniejących certificateorder|
|/certificateOrders/renew/Action|Odnów istniejący certificateorder|
|/certificateOrders/retrieveCertificateActions/Action|Pobieranie listy hello akcji certyfikatu|
|/certificateOrders/retrieveEmailHistory/Action|Pobieranie certyfikatu historii wiadomości e-mail|
|/certificateOrders/resendEmail/Action|Ponowne wysyłanie wiadomości e-mail certyfikatu|
|/certificateOrders/verifyDomainOwnership/Action|Zweryfikuj prawo własności do domeny|
|/certificateOrders/resendRequestEmails/Action|Żądanie ponownego wysłania wiadomości e-mail adres e-mail tooanother|
|/certificateOrders/resendRequestEmails/Action|Pobrać zamknięcia lokacji w celu wystawiony certyfikat usługi aplikacji|
|/certificateOrders/Certificates/Write|Dodaj nowy certyfikat lub zaktualizuj istniejącą|
|/certificateOrders/Certificates/DELETE|Usuń istniejący certyfikat|
|/certificateOrders/Certificates/Read|Pobierz listę hello certyfikatów|

## <a name="microsoftclassiccompute"></a>Obszar Microsoft.ClassicCompute

| Operacja | Opis |
|---|---|
|/ register/działania|Zarejestruj tooClassic obliczeń|
|/ checkDomainNameAvailability/działania|Sprawdza dostępność hello danej nazwy domeny.|
|/ moveSubscriptionResources/działania|Przenieś wszystkie zasoby klasyczne tooa innej subskrypcji.|
|/ validateSubscriptionMoveAvailability/działania|Sprawdzanie poprawności subskrypcji hello dostępności dla operacji przenoszenia klasycznego.|
|/operatingSystemFamilies/Read|Zawiera listę rodzin systemu operacyjnego gościa hello dostępnych w Microsoft Azure, a także wymieniono wersje systemu operacyjnego hello dostępne dla każdego f
|/Capabilities/Read|Pokazuje możliwości hello|
|/operatingSystems/Read|Wyświetla listę hello wersji systemu operacyjnego gościa hello, które są obecnie dostępne w systemie Microsoft Azure.|
|/resourceTypes/skus/Read|Pobiera listę jednostek Sku hello obsługiwane typy zasobów.|
|/domainNames/Read|Zwróć hello nazwy domen dla zasobów.|
|/ domainNames/zapisu|Dodaje lub modyfikuje hello nazwy domen dla zasobów.|
|/domainNames/DELETE|Usuń hello nazwy domen dla zasobów.|
|/domainNames/swap/Action|Zamienia hello miejsca produkcji toohello miejsca.|
|/domainNames/serviceCertificates/Read|Zwraca hello używane certyfikaty usługi.|
|/domainNames/serviceCertificates/Write|Dodaje lub modyfikuje używane certyfikaty usługi hello.|
|/domainNames/serviceCertificates/DELETE|Usuń używane certyfikaty usługi hello.|
|/domainNames/serviceCertificates/operationStatuses/Read|Odczytuje hello stan operacji dla certyfikatów usługi nazw domeny hello.|
|/domainNames/Capabilities/Read|Pokazuje możliwości nazwy domeny hello|
|/domainNames/Extensions/Read|Zwraca hello rozszerzenia nazwy domeny.|
|/domainNames/Extensions/Write|Dodanie rozszerzenia nazwy domeny hello.|
|/domainNames/Extensions/DELETE|Usuń rozszerzenia nazwy domeny hello.|
|/domainNames/Extensions/operationStatuses/Read|Odczytuje stan operacji powitania dla rozszerzenia nazwy domeny hello.|
|/domainNames/Active/Write|Ustawia nazwę aktywnej domeny hello.|
|/domainNames/Slots/Read|Pokazuje hello miejsc wdrożenia.|
|/domainNames/Slots/Write|Tworzy lub aktualizuje hello wdrożenia.|
|/domainNames/Slots/DELETE|Usuwa dane miejsce wdrożenia.|
|/domainNames/Slots/Start/Action|Uruchamia miejsce wdrożenia.|
|/domainNames/Slots/Stop/Action|Wstrzymuje hello miejsca wdrożenia.|
|/domainNames/Slots/operationStatuses/Read|Odczytuje hello stan operacji dla gniazd nazw domen hello.|
|/domainNames/Slots/Roles/Read|Pobierz hello roli miejsca wdrożenia hello.|
|/domainNames/Slots/Roles/extensionReferences/Read|Zwraca hello odwołania do rozszerzenia dla roli miejsca wdrożenia hello.|
|/domainNames/Slots/Roles/extensionReferences/Write|Dodaje lub modyfikuje hello odwołania do rozszerzenia roli miejsca wdrożenia hello.|
|/domainNames/Slots/Roles/extensionReferences/DELETE|Usuń hello odwołania do rozszerzenia roli miejsca wdrożenia hello.|
|/domainNames/Slots/Roles/extensionReferences/operationStatuses/Read|Odczytuje hello stan operacji dla odwołań rozszerzenia ról gniazd nazw hello domeny.|
|/domainNames/Slots/Roles/roleInstances/Read|Pobierz hello wystąpienia roli.|
|/domainNames/Slots/Roles/roleInstances/restart/Action|Ponowne uruchomienie wystąpienia roli.|
|/domainNames/Slots/Roles/roleInstances/reimage/Action|Wystąpienie roli hello reimages.|
|/domainNames/Slots/Roles/roleInstances/operationStatuses/Read|Odczytuje hello stan operacji dla wystąpień roli ról gniazd nazw hello domeny.|
|/domainNames/Slots/State/Start/Write|Zmiany hello toostopped stan miejsca wdrożenia.|
|/domainNames/Slots/State/Stop/Write|Zmiany hello toostarted stan miejsca wdrożenia.|
|/domainNames/Slots/upgradeDomain/Write|Przeprowadź hello uaktualnienia domeny.|
|/domainNames/internalLoadBalancers/Read|Pobiera hello wewnętrzne moduły równoważenia obciążenia.|
|/domainNames/internalLoadBalancers/Write|Tworzy nową wewnętrzną usługę równoważenia obciążenia.|
|/domainNames/internalLoadBalancers/DELETE|Usuwa nową wewnętrzną usługę równoważenia obciążenia.|
|/domainNames/internalLoadBalancers/operationStatuses/Read|Odczytuje stan operacji powitania dla nazw domen hello wewnętrzne moduły równoważenia obciążenia.|
|/domainNames/loadBalancedEndpointSets/Read|Pokazuje zestawy punktów końcowych ze zrównoważonym obciążeniem hello|
|/domainNames/loadBalancedEndpointSets/operationStatuses/Read|Odczytuje stan operacji powitania dla nazw domen hello zestawy punktów końcowych ze zrównoważonym obciążeniem.|
|/domainNames/availabilitySets/Read|Pokaż hello zbiór dostępności dla zasobu hello.|
|/Quotas/Read|Pobierz hello przydziału dla subskrypcji hello.|
|/virtualMachines/Read|Pobiera listę maszyn wirtualnych.|
|/ virtualMachines/zapisu|Dodaje lub modyfikuje maszyny wirtualne.|
|/virtualMachines/DELETE|Usuwa maszyn wirtualnych.|
|/virtualMachines/Start/Action|Uruchom maszynę wirtualną hello.|
|/virtualMachines/redeploy/Action|Wdraża ponownie hello maszyny wirtualnej.|
|/virtualMachines/restart/Action|Ponowne uruchomienie maszyn wirtualnych.|
|/virtualMachines/Stop/Action|Zatrzymuje hello maszyny wirtualnej.|
|/virtualMachines/shutdown/Action|Maszyna wirtualna hello zamknięcia.|
|/virtualMachines/attachDisk/Action|Dołącza maszynę wirtualną tooa dysku danych.|
|/virtualMachines/detachDisk/Action|Odłącza dysk z danymi od maszyny wirtualnej.|
|/virtualMachines/downloadRemoteDesktopConnectionFile/Action|Pobiera hello plik RDP dla maszyny wirtualnej.|
|/virtualMachines/Networkinterface /<br>associatedNetworkSecurityGroups/Odczyt|Pobiera hello sieciową grupę zabezpieczeń skojarzoną z interfejsem sieciowym hello.|
|/virtualMachines/Networkinterface /<br>associatedNetworkSecurityGroups/zapisu|Dodaje sieciową grupę zabezpieczeń skojarzoną z interfejsem sieci hello.|
|/virtualMachines/Networkinterface /<br>associatedNetworkSecurityGroups/usuwania|Usuwa hello sieciową grupę zabezpieczeń skojarzoną z interfejsem sieciowym hello.|
|/virtualMachines/Networkinterface /<br>associatedNetworkSecurityGroups operationStatuses/odczytu|Odczytuje stan operacji hello maszyn wirtualnych hello skojarzonych grup zabezpieczeń sieci.|
|/virtualMachines/Providers/Microsoft.Insights/metricDefinitions/Read|Pobiera definicje metryk hello.|
|/virtualMachines/Providers/Microsoft.Insights/diagnosticSettings/Read|Pobierz ustawienia diagnostyki hello.|
|/virtualMachines/Providers/Microsoft.Insights/diagnosticSettings/Write|Dodaje lub modyfikuje ustawienia diagnostyczne.|
|/virtualMachines/Metrics/Read|Pobiera hello metryki.|
|/virtualMachines/operationStatuses/Read|Odczytuje stan operacji hello hello maszyn wirtualnych.|
|/virtualMachines/Extensions/Read|Pobiera hello rozszerzenie maszyny wirtualnej.|
|/virtualMachines/Extensions/Write|Umieszcza rozszerzenie maszyny wirtualnej hello.|
|/virtualMachines/Extensions/operationStatuses/Read|Odczytuje stan operacji hello hello rozszerzeń maszyny wirtualnej.|
|/virtualMachines/asyncOperations/Read|Pobiera hello dostępne operacje asynchroniczne|
|/virtualMachines/Disks/Read|Pobiera listę dysków z danymi|
|/virtualMachines/associatedNetworkSecurityGroups/Read|Pobiera hello sieciową grupę zabezpieczeń skojarzoną z maszyną wirtualną hello.|
|/virtualMachines/associatedNetworkSecurityGroups/Write|Dodaje sieciową grupę zabezpieczeń skojarzoną z maszyną wirtualną hello.|
|/virtualMachines/associatedNetworkSecurityGroups/DELETE|Usuwa hello sieciową grupę zabezpieczeń skojarzoną z maszyną wirtualną hello.|
|/virtualMachines/associatedNetworkSecurityGroups/operationStatuses/Read|Odczytuje stan operacji hello maszyn wirtualnych hello skojarzonych grup zabezpieczeń sieci.|

## <a name="microsoftclassicnetwork"></a>Microsoft.ClassicNetwork

| Operacja | Opis |
|---|---|
|/ register/działania|Zarejestruj tooClassic sieci|
|/gatewaySupportedDevices/Read|Pobiera hello listę obsługiwanych urządzeń.|
|/reservedIps/Read|Pobiera hello zastrzeżonych adresów IP|
|/ zastrzeżonych adresów IP/zapisu|Dodaje nowy zastrzeżony adres IP|
|/reservedIps/DELETE|Usuwa zastrzeżony adres IP.|
|/reservedIps/Link/Action|Połącz zarezerwowany adres IP|
|/reservedIps/JOIN/Action|Dołącz zarezerwowany adres IP|
|/reservedIps/operationStatuses/Read|Odczytuje stan operacji hello hello zarezerwowanych adresów IP.|
|/virtualNetworks/Read|Pobierz hello sieci wirtualnej.|
|/ virtualNetworks/zapisu|Dodaje nową sieć wirtualną.|
|/virtualNetworks/DELETE|Usuwa hello sieci wirtualnej.|
|/virtualNetworks/peer/Action|Łączy równorzędnie sieć wirtualną z inną siecią wirtualną.|
|/virtualNetworks/JOIN/Action|Tworzy sprzężenie hello sieci wirtualnej.|
|/virtualNetworks/checkIPAddressAvailability/Action|Sprawdza dostępność hello z danego adresu IP w sieci wirtualnej.|
|/virtualNetworks/Capabilities/Read|Pokazuje możliwości hello|
|/virtualNetworks/podsieci /<br>associatedNetworkSecurityGroups/Odczyt|Pobiera hello sieciową grupę zabezpieczeń skojarzoną z podsiecią hello.|
|/virtualNetworks/podsieci /<br>associatedNetworkSecurityGroups/zapisu|Dodaje grupę zabezpieczeń sieci skojarzonych z hello podsieci.|
|/virtualNetworks/podsieci /<br>associatedNetworkSecurityGroups/usuwania|Usuwa hello sieciową grupę zabezpieczeń skojarzoną z podsiecią hello.|
|/virtualNetworks/podsieci /<br>associatedNetworkSecurityGroups operationStatuses/odczytu|Odczytuje stan operacji powitania dla grupy zabezpieczeń sieci skojarzonej z podsiecią w podsieci sieci wirtualnej hello.|
|/virtualNetworks/operationStatuses/Read|Odczytuje stan operacji hello hello wirtualnych sieci.|
|/virtualNetworks/Gateways/Read|Pobiera hello bram sieci wirtualnej.|
|/virtualNetworks/Gateways/Write|Dodaje bramę sieci wirtualnej.|
|/virtualNetworks/Gateways/DELETE|Usuwa hello bramy sieci wirtualnej.|
|/virtualNetworks/Gateways/startDiagnostics/Action|Uruchamia diagnostykę bramy sieci wirtualnej hello.|
|/virtualNetworks/Gateways/stopDiagnostics/Action|Zatrzymuje hello diagnostykę bramy sieci wirtualnej hello.|
|/virtualNetworks/Gateways/downloadDiagnostics/Action|Pobiera hello diagnostyki bramy.|
|/virtualNetworks/Gateways/listCircuitServiceKey/Action|Pobiera klucz usługi obwodu hello.|
|/virtualNetworks/Gateways/downloadDeviceConfigurationScript/Action|Pobiera skrypt konfiguracji urządzenia hello.|
|/virtualNetworks/Gateways/listPackage/Action|Wyświetla pakiet bramy sieci wirtualnej hello.|
|/virtualNetworks/Gateways/operationStatuses/Read|Odczytuje stan operacji hello hello bram sieci wirtualnych.|
|/virtualNetworks/Gateways/Packages/Read|Pobiera pakiet bramy sieci wirtualnej hello.|
|/virtualNetworks/Gateways/Connections/Read|Pobiera listę hello połączeń.|
|/virtualNetworks/Gateways/Connections/Connect/Action|Umożliwia nawiązanie połączenia bramy toosite witryny.|
|/virtualNetworks/Gateways/Connections/Disconnect/Action|Rozłącza połączenie bramy toosite lokacji.|
|/virtualNetworks/Gateways/Connections/test/Action|Testuje połączenie bramy toosite lokacji.|
|/virtualNetworks/Gateways/clientRevokedCertificates/Read|Witaj odczytu odwołane certyfikaty klienta.|
|/virtualNetworks/Gateways/clientRevokedCertificates/Write|Cofa certyfikat klienta.|
|/virtualNetworks/Gateways/clientRevokedCertificates/DELETE|Odwołuje cofnięcie certyfikatu klienta.|
|/virtualNetworks/Gateways/clientRootCertificates/Read|Znajdź hello certyfikaty główne klienta.|
|/virtualNetworks/Gateways/clientRootCertificates/Write|Przekazuje nowy certyfikat główny klienta.|
|/virtualNetworks/Gateways/clientRootCertificates/DELETE|Usuwa certyfikat klienta bramy sieci wirtualnej hello.|
|/virtualNetworks/Gateways/clientRootCertificates/Download/Action|Pobiera certyfikat na podstawie odcisku palca.|
|/virtualNetworks/Gateways/clientRootCertificates/listPackage/Action|Wyświetla pakiet certyfikatu bramy sieci wirtualnej hello.|
|/networkSecurityGroups/Read|Pobiera hello sieciowej grupy zabezpieczeń.|
|/ Networksecuritygroup/zapisu|Dodaje nową sieciową grupę zabezpieczeń.|
|/networkSecurityGroups/DELETE|Usuwa grupę zabezpieczeń sieci hello.|
|/networkSecurityGroups/operationStatuses/Read|Odczytuje stan operacji hello hello sieciowej grupy zabezpieczeń.|
|/networkSecurityGroups/securityRules/Read|Pobiera hello regułę zabezpieczeń.|
|/networkSecurityGroups/securityRules/Write|Dodaje lub aktualizuje regułę zabezpieczeń.|
|/networkSecurityGroups/securityRules/DELETE|Usuwa regułę zabezpieczeń hello.|
|/networkSecurityGroups/securityRules/operationStatuses/Read|Odczytuje hello stan operacji dla reguł zabezpieczeń grupy zabezpieczeń sieci hello.|
|/Quotas/Read|Pobierz hello przydziału dla subskrypcji hello.|

## <a name="microsoftclassicstorage"></a>Microsoft.ClassicStorage

| Operacja | Opis |
|---|---|
|/ register/działania|Zarejestruj tooClassic magazynu|
|/ checkStorageAccountAvailability/działania|Sprawdza dostępność hello konta magazynu.|
|/Capabilities/Read|Pokazuje możliwości hello|
|/publicImages/Read|Pobiera hello obraz publicznego maszyny wirtualnej.|
|/images/Read|Zwraca obraz powitania.|
|/storageAccounts/Read|Zwróć hello konta magazynu z hello danego konta.|
|/ storageAccounts/zapisu|Dodaje nowe konto magazynu.|
|/storageAccounts/DELETE|Usunięcie konta magazynu hello.|
|/storageAccounts/listKeys/Action|Wyświetla listę hello klucze dostępu dla konta magazynu hello.|
|/storageAccounts/regenerateKey/Action|Generuje ponownie hello istniejące klucze dostępu dla konta magazynu hello.|
|/storageAccounts/operationStatuses/Read|Odczytuje stan operacji hello hello zasobu.|
|/storageAccounts/images/Read|Zwraca hello obraz konta magazynu.|
|/storageAccounts/images/DELETE|Usuwa określony obraz konta magazynu.|
|/storageAccounts/Disks/Read|Zwraca hello dysku konta magazynu.|
|/storageAccounts/Disks/Write|Dodaje dysk konta magazynu.|
|/storageAccounts/Disks/DELETE|Usuwa dany dysk konta magazynu.|
|/storageAccounts/Disks/operationStatuses/Read|Odczytuje stan operacji hello hello zasobu.|
|/storageAccounts/osImages/Read|Zwraca hello obraz systemu operacyjnego konta magazynu.|
|/storageAccounts/osImages/DELETE|Usuwa określony obraz systemu operacyjnego konta magazynu.|
|/storageAccounts/Services/Read|Pobierz hello dostępnych usług.|
|/storageAccounts/Services/metricDefinitions/Read|Pobiera definicje metryk hello.|
|/storageAccounts/Services/Metrics/Read|Pobiera hello metryki.|
|/storageAccounts/Services/diagnosticSettings/Read|Pobierz ustawienia diagnostyki hello.|
|/storageAccounts/Services/diagnosticSettings/Write|Dodaje lub modyfikuje ustawienia diagnostyczne.|
|/Disks/Read|Zwraca hello dysku konta magazynu.|
|/osImages/Read|Zwraca obraz systemu operacyjnego hello.|
|/Quotas/Read|Pobierz hello przydziału dla subskrypcji hello.|

## <a name="microsoftcognitiveservices"></a>Microsoft.CognitiveServices

| Operacja | Opis |
|---|---|
|/accounts/Read|Odczytuje kont interfejsu API.|
|/ kont/zapisu|Zapisuje kont interfejsu API.|
|/accounts/DELETE|Usuwa konta interfejsu API|
|/accounts/listKeys/Action|Lista kluczy|
|/accounts/regenerateKey/Action|Ponowne generowanie klucza|
|/accounts/skus/Read|Odczytuje dostępne jednostki SKU dla istniejącego zasobu.|
|/accounts/Usages/Read|Pobierz użycie przydziału hello istniejącego zasobu.|
|Operacje/odczytu|Opis operacji hello.|

## <a name="microsoftcommerce"></a>Microsoft.Commerce

| Operacja | Opis |
|---|---|
|RateCard/odczytu|Zwraca oferują danych, metadane Miernik/zasobów i szybkości dla hello podanej subskrypcji.|
|UsageAggregates/odczytu|Pobiera Microsoft Azure — użytek przez subskrypcję. wynik Hello zawiera agreguje dane dotyczące użycia, subskrypcji i zasobu powiązane informacje, w określonym czasie.|

## <a name="microsoftcompute"></a>Microsoft.Compute

| Operacja | Opis |
|---|---|
|/ register/działania|Rejestruje subskrypcję za pomocą dostawcy zasobów Microsoft.Compute|
|/restorePointCollections/Read|Pobierz właściwości hello kolekcji punktu przywracania|
|/ restorePointCollections/zapisu|Tworzy nową kolekcję punkt przywracania, lub aktualizuje istniejący zestaw|
|/restorePointCollections/DELETE|Usuwa hello kolekcji punktu przywracania i zawiera punkty przywracania|
|/restorePointCollections/restorePoints/Read|Pobierz właściwości hello punktu przywracania|
|/restorePointCollections/restorePoints/Write|Tworzy nowy punkt przywracania|
|/restorePointCollections/restorePoints/DELETE|Usuwa hello punkt przywracania|
|/restorePointCollections/restorePoints/retrieveSasUris/Action|Pobierz właściwości hello punktu przywracania oraz identyfikatorów URI SAS obiektu blob|
|/virtualMachineScaleSets/Read|Pobierz właściwości hello zestawu skali maszyny wirtualnej|
|/ virtualMachineScaleSets/zapisu|Tworzy nowy zestaw skali maszyny wirtualnej lub aktualizuje istniejący zestaw|
|/virtualMachineScaleSets/DELETE|Usuwa zestaw skali maszyny wirtualnej hello|
|/virtualMachineScaleSets/Start/Action|Uruchamia hello wystąpienia zestawu skali maszyny wirtualnej hello|
|/virtualMachineScaleSets/powerOff/Action|Wyłącza wystąpienia zestawu skali maszyny wirtualnej hello hello|
|/virtualMachineScaleSets/restart/Action|Uruchamia ponownie wystąpienia zestawu skali maszyny wirtualnej hello hello|
|/virtualMachineScaleSets/deallocate/Action|Wyłącza i zwalnia zasoby obliczeniowe hello hello wystąpienia zestawu skali maszyny wirtualnej hello |
|/virtualMachineScaleSets/manualUpgrade/Action|Ręcznie aktualizuje wystąpienia toolatest modelu zestawu skali maszyny wirtualnej hello|
|/virtualMachineScaleSets/Scale/Action|Skalowanie w / set Skaluj w poziomie liczby wystąpień istniejących skalowania maszyny wirtualnej|
|/virtualMachineScaleSets/instanceView/Read|Pobiera widok wystąpienia zestawu skali maszyny wirtualnej hello hello|
|/virtualMachineScaleSets/skus/Read|Wyświetla hello prawidłowe jednostki SKU dla istniejącego zestawu skalowania maszyny wirtualnej|
|/virtualMachineScaleSets/virtualMachines/Read|Pobiera właściwości hello maszyny wirtualnej w zestawie skalowania maszyn wirtualnych|
|/virtualMachineScaleSets/virtualMachines/DELETE|Usuń konkretną maszynę wirtualną z zestawu skalowania maszyn wirtualnych.|
|/virtualMachineScaleSets/virtualMachines/Start/Action|Uruchamia wystąpienie maszyny wirtualnej w zestawie skalowania maszyn wirtualnych.|
|/virtualMachineScaleSets/virtualMachines/powerOff/Action|Wyłącza wystąpienie maszyny wirtualnej w zestawie skalowania maszyn wirtualnych.|
|/virtualMachineScaleSets/virtualMachines/restart/Action|Uruchamia ponownie wystąpienie maszyny wirtualnej w zestawie skalowania maszyn wirtualnych.|
|/virtualMachineScaleSets/virtualMachines/deallocate/Action|Wyłącza i zwalnia zasoby obliczeniowe hello dla maszyny wirtualnej w zestawie skalowania maszyn wirtualnych.|
|/virtualMachineScaleSets/virtualMachines/instanceView/Read|Pobiera widok wystąpienia hello maszyny wirtualnej w zestawie skalowania maszyn wirtualnych.|
|/images/Read|Pobierz właściwości hello hello obrazu|
|/ obrazów/zapisu|Tworzy nowy obraz lub aktualizuje istniejący zestaw|
|/images/DELETE|Usuwa obraz powitania|
|/Operations/Read|Wyświetla operacje dostępne dla dostawcy zasobów Microsoft.Compute|
|/Disks/Read|Pobierz właściwości hello dysku|
|/ dysków/zapisu|Tworzy nowy dysk lub aktualizuje istniejący|
|/Disks/DELETE|Usuwa hello dysku|
|/Disks/beginGetAccess/Action|Pobierz hello identyfikator URI sygnatury dostępu Współdzielonego hello dysku dla dostępu do obiektów blob|
|/Disks/endGetAccess/Action|Odwołaj hello identyfikator URI sygnatury dostępu Współdzielonego hello dysku|
|/snapshots/Read|Pobierz właściwości hello migawki|
|/ migawek/zapisu|Utwórz nową migawkę lub zaktualizuj istniejącą|
|/snapshots/DELETE|Usuń migawkę|
|/availabilitySets/Read|Pobierz właściwości hello zestawu dostępności|
|/ availabilitySets/zapisu|Tworzy nowy zestaw dostępności lub aktualizuje istniejący zestaw|
|/availabilitySets/DELETE|Usuwa zestaw dostępności hello|
|/availabilitySets/vmSizes/Read|Wyświetl dostępne rozmiary do tworzenia lub aktualizowania maszyny wirtualnej w zestawie dostępności hello|
|/virtualMachines/Read|Pobierz właściwości hello maszyny wirtualnej|
|/ virtualMachines/zapisu|Tworzy nową maszynę wirtualną lub aktualizuje istniejącą maszynę wirtualną|
|/virtualMachines/DELETE|Usuwa hello maszyny wirtualnej|
|/virtualMachines/Start/Action|Maszyna wirtualna uruchamia hello|
|/virtualMachines/powerOff/Action|Wyłącza hello maszyny wirtualnej. Należy pamiętać, że hello maszyny wirtualnej będzie rozliczane toobe.|
|/virtualMachines/redeploy/Action|Wdraża ponownie maszyny wirtualnej|
|/virtualMachines/restart/Action|Uruchamia ponownie hello maszyny wirtualnej|
|/virtualMachines/deallocate/Action|Wyłącza hello maszynę wirtualną i zwalnia hello zasoby obliczeniowe|
|/virtualMachines/generalize/Action|Ustawia tooGeneralized stan maszyny wirtualnej hello i przygotowuje hello maszynę wirtualną do przechwycenia|
|/virtualMachines/Capture/Action|Przechwytuje maszynę wirtualną hello przez kopiowanie wirtualnych dysków twardych oraz generuje szablon, który może być używane toocreate podobnych maszyn wirtualnych|
|/virtualMachines/convertToManagedDisks/Action|Konwertuje hello na podstawie obiektu blob dysków hello maszyny wirtualnej toomanaged dysków|
|/virtualMachines/vmSizes/Read|Wyświetla dostępne rozmiary, które można zaktualizować hello maszyny wirtualnej|
|/virtualMachines/instanceView/Read|Pobiera hello szczegółowy stan środowiska uruchomieniowego hello maszyny wirtualnej i jej zasobów|
|/virtualMachines/Extensions/Read|Pobierz właściwości hello rozszerzenia maszyny wirtualnej|
|/virtualMachines/Extensions/Write|Tworzy nowe rozszerzenie maszyny wirtualnej lub aktualizuje istniejące rozszerzenie|
|/virtualMachines/Extensions/DELETE|Usuwa rozszerzenie maszyny wirtualnej hello|
|/Locations/vmSizes/Read|Wyświetla listę dostępnych rozmiarów maszyny wirtualnej w danej lokalizacji|
|/Locations/Usages/Read|Pobiera limity usług i bieżące użycie ilości zasobów obliczeniowych subskrypcji hello w lokalizacji|
|/Locations/Operations/Read|Pobiera stan hello operacji asynchronicznej|

## <a name="microsoftcontainerregistry"></a>Microsoft.ContainerRegistry

| Operacja | Opis |
|---|---|
|/ register/działania|Rejestruje subskrypcję dostawcy zasobów rejestru kontenera hello hello i umożliwia tworzenie hello rejestrów kontenera.|
|/checknameavailability/Read|Sprawdza się, że nazwa rejestru jest prawidłowa i nie jest używany.|
|/registries/Read|Zwraca hello lista rejestrów kontenera lub pobiera hello właściwości hello rejestru określonego kontenera.|
|/ rejestrów/zapisu|Tworzy kontener rejestru z hello określonych parametrów lub zaktualizuj właściwości hello lub tagi dla hello rejestru określonego kontenera.|
|/registries/DELETE|Usuwa istniejące rejestru kontenera.|
|/registries/listCredentials/Action|Wyświetla listę hello poświadczenia logowania dla hello rejestru określonego kontenera.|
|/registries/regenerateCredential/Action|Generuje ponownie hello poświadczenia logowania dla hello rejestru określonego kontenera.|

## <a name="microsoftcontainerservice"></a>Microsoft.ContainerService

| Operacja | Opis |
|---|---|
|/containerServices/Subscriptions/Read|Get hello określone usługi kontenerów na podstawie subskrypcji|
|/containerServices/resourceGroups/Read|Get hello określone usługi kontenerów na podstawie grupy zasobów|
|/containerServices/resourceGroups/ContainerServiceName/Read|Pobiera hello określone usługi kontenera|
|/containerServices/resourceGroups/ContainerServiceName/Write|Określony kontener usługi naraża lub hello aktualizacji|
|/containerServices/resourceGroups/ContainerServiceName/DELETE|Usuwa hello określone usługi kontenera|

## <a name="microsoftcontentmoderator"></a>Microsoft.ContentModerator

| Operacja | Opis |
|---|---|
|/ updateCommunicationPreference/działania|Preferencji komunikacji aktualizacji|
|/ listCommunicationPreference/działania|Lista komunikacji preferencji|
|/Applications/Read|Operacja odczytu|
|/ applications/zapisu|Operacja zapisu|
|/ applications/zapisu|Operacja zapisu|
|/Applications/DELETE|Operacja usuwania|
|/Applications/listSecrets/Action|Utwórz listę kluczy tajnych|
|/Applications/listSingleSignOnToken/Action|Odczyt jednokrotnego tokenów|
|/Operations/Read|operacje odczytu|

## <a name="microsoftcustomerinsights"></a>Microsoft.CustomerInsights

| Operacja | Opis |
|---|---|
|/hubs/Read|Przeczytaj dowolnego Centrum Insights Azure klienta|
|/ hubs/zapisu|Utwórz lub zaktualizuj Centrum Insights dowolnego klienta usługi Azure|
|/hubs/DELETE|Usunąć wszelkie Centrum Insights klienta platformy Azure|
|/hubs/Providers/Microsoft.Insights/metricDefinitions/Read|Pobiera hello dostępne metryki dla zasobu|
|/hubs/Providers/Microsoft.Insights/diagnosticSettings/Read|Pobiera hello ustawienie diagnostyczne dla zasobu hello|
|/hubs/Providers/Microsoft.Insights/diagnosticSettings/Write|Tworzy lub aktualizuje hello ustawienie diagnostyczne dla zasobu hello|
|/hubs/Providers/Microsoft.Insights/logDefinitions/Read|Pobiera dostępne dzienniki powitania dla zasobu|
|/hubs/authorizationPolicies/Read|Przeczytaj zasady podpisu dostępu udostępniony żadnych informacji szczegółowych Azure klienta|
|/hubs/authorizationPolicies/Write|Utwórz lub zaktualizuj dowolne zasady sygnatury dostępu współdzielonego Insights klienta Azure|
|/hubs/authorizationPolicies/DELETE|Usuń dowolne zasady sygnatury dostępu współdzielonego Insights klienta platformy Azure|
|/hubs/authorizationPolicies/regeneratePrimaryKey/Action|Ponowne wygenerowanie klucza podstawowego Azure klienta Insights zasad dostępu współużytkowanego podpisu|
|/hubs/authorizationPolicies/regenerateSecondaryKey/Action|Ponowne wygenerowanie klucza pomocniczego Azure klienta Insights zasad dostępu współużytkowanego podpisu|
|/hubs/Profiles/Read|Przeczytaj dowolnego profilu Insights klienta platformy Azure|
|/hubs/Profiles/Write|Zapis dowolnego profilu Insights klienta platformy Azure|
|/hubs/KPI/Read|Przeczytaj dowolnego klienta Azure Insights kluczowy wskaźnik wydajności|
|/hubs/KPI/Write|Utwórz lub zaktualizuj dowolnego klienta Azure Insights kluczowy wskaźnik wydajności|
|/hubs/KPI/DELETE|Usuń wszelkie klienta Azure Insights kluczowy wskaźnik wydajności|
|/hubs/views/Read|Przeczytaj dowolnym widoku App Insights klienta usługi Azure|
|/hubs/views/Write|Utwórz lub zaktualizuj dowolnym widoku App Insights klienta usługi Azure|
|/hubs/views/DELETE|Usuń wszelkie widok aplikacji Insights klienta usługi Azure|
|/hubs/Interactions/Read|Przeczytaj interakcji Insights klienta platformy Azure|
|/hubs/Interactions/Write|Utwórz lub zaktualizuj interakcji Insights klienta platformy Azure|
|/hubs/roleAssignments/Read|Przeczytaj przydziału Rbac Insights klienta platformy Azure|
|/hubs/roleAssignments/Write|Utwórz lub zaktualizuj wszystkie przypisania Rbac Insights klienta Azure|
|/hubs/roleAssignments/DELETE|Usuń wszelkie przydział Rbac Insights klienta Azure|
|/hubs/Connectors/Read|Każdy łącznik Insights Azure klienta do odczytu|
|/hubs/Connectors/Write|Utwórz lub zaktualizuj każdy łącznik Insights klienta platformy Azure|
|/hubs/Connectors/DELETE|Usunięcie łącznika Insights dowolnego klienta platformy Azure|
|/hubs/Connectors/Mappings/Read|Przeczytaj żadnego mapowania łącznika Insights klienta platformy Azure|
|/hubs/Connectors/Mappings/Write|Utwórz lub zaktualizuj żadnego mapowania łącznika Insights klienta platformy Azure|
|/hubs/Connectors/Mappings/DELETE|Usunąć wszystkie mapowania łącznika Insights klienta Azure|

## <a name="microsoftdatacatalog"></a>Microsoft.DataCatalog

| Operacja | Opis |
|---|---|
|/ checkNameAvailability/działania|Służy do sprawdzania dostępności nazwy katalogu dla dzierżawcy.|
|/Catalogs/Read|Pobierz właściwości dla katalogu lub katalogów w ramach subskrypcji lub grupy zasobów.|
|/ wykazów/zapisu|Tworzy znaczniki hello katalogu lub aktualizacje i właściwości hello katalogu.|
|/Catalogs/DELETE|Usuwa hello katalogu.|

## <a name="microsoftdatafactory"></a>Microsoft.DataFactory

| Operacja | Opis |
|---|---|
|/datafactories/Read|Odczytuje fabryki danych.|
|/ datafactories/zapisu|Utwórz lub zaktualizuj fabryki danych|
|/datafactories/DELETE|Usuwa fabryki danych.|
|/datafactories/datapipelines/Read|Odczytuje potoku.|
|/datafactories/datapipelines/DELETE|Usuwa potoku.|
|/datafactories/datapipelines/pause/Action|Potok pauzy.|
|/datafactories/datapipelines/resume/Action|Wznawia potoku.|
|/datafactories/datapipelines/Update/Action|Potoku aktualizacji.|
|/datafactories/datapipelines/Write|Utwórz lub zaktualizuj potoku|
|/datafactories/linkedServices/Read|Odczytuje połączonej usługi.|
|/datafactories/linkedServices/DELETE|Usuwa połączonej usługi.|
|/datafactories/linkedServices/Write|Tworzenie lub aktualizacja połączonej usługi|
|/datafactories/Tables/Read|Odczytuje tabeli.|
|/datafactories/Tables/DELETE|Usuwa tabelę.|
|/datafactories/Tables/Write|Utwórz lub zaktualizuj tabelę|

## <a name="microsoftdatalakeanalytics"></a>Microsoft.DataLakeAnalytics

| Operacja | Opis |
|---|---|
|/accounts/Read|Pobiera informacje o hello DataLakeAnalytics konta.|
|/ kont/zapisu|Utwórz lub zaktualizuj konto DataLakeAnalytics hello.|
|/accounts/DELETE|Usuwanie konta DataLakeAnalytics hello.|
|/accounts/firewallRules/Read|Pobierz informacje dotyczące reguły zapory.|
|/accounts/firewallRules/Write|Utwórz lub zaktualizuj regułę zapory.|
|/accounts/firewallRules/DELETE|Usuwanie reguły zapory.|
|/accounts/storageAccounts/Read|Pobierz hello DataLakeAnalytics konto połączonego konta magazynu.|
|/accounts/storageAccounts/Write|Połącz toohello konta magazynu DataLakeAnalytics konta.|
|/accounts/storageAccounts/DELETE|Odłącz od hello DataLakeAnalytics konta przy użyciu konta magazynu.|
|/accounts/storageAccounts/containers/Read|Pobierz kontenery w obszarze hello konta magazynu|
|/accounts/storageAccounts/containers/listSasTokens/Action|Listy tokenów SAS dla kontenera magazynu hello|
|/accounts/dataLakeStoreAccounts/Read|Pobierz połączonego konta DataLakeStore hello DataLakeAnalytics konta.|
|/accounts/dataLakeStoreAccounts/Write|Połącz toohello konta DataLakeStore DataLakeAnalytics konta.|
|/accounts/dataLakeStoreAccounts/DELETE|Odłącz od hello DataLakeAnalytics konta przy użyciu konta DataLakeStore.|

## <a name="microsoftdatalakestore"></a>Microsoft.DataLakeStore

| Operacja | Opis |
|---|---|
|/accounts/Read|Pobiera informacje o istniał już konto DataLakeStore.|
|/ kont/zapisu|Utwórz nowe konto DataLakeStore lub zaktualizuj konto istniał już DataLakeStore.|
|/accounts/DELETE|Usuń konto istniał już DataLakeStore.|
|/accounts/firewallRules/Read|Pobierz informacje dotyczące reguły zapory.|
|/accounts/firewallRules/Write|Utwórz lub zaktualizuj regułę zapory.|
|/accounts/firewallRules/DELETE|Usuwanie reguły zapory.|
|/accounts/trustedIdProviders/Read|Pobiera informacje o zaufanego dostawcę tożsamości.|
|/accounts/trustedIdProviders/Write|Utwórz lub zaktualizuj zaufanego dostawcę tożsamości.|
|/accounts/trustedIdProviders/DELETE|Usuń zaufanego dostawcę tożsamości.|

## <a name="microsoftdevices"></a>Microsoft.Devices

| Operacja | Opis |
|---|---|
|/ register/działania|Zarejestruj subskrypcję hello hello Centrum IotHub zasobów dostawcy i umożliwia hello tworzenie zasobów Centrum IotHub|
|/ checkNameAvailability/działania|Sprawdź, czy jest dostępna nazwa Jeśli Centrum IotHub|
|/ użycia/odczytu|Uzyskanie subskrypcji Szczegóły obciążenia dla tego dostawcy.|
|/ operations/odczytu|Pobierz wszystkie operacje ResourceProvider|
|/ iotHubs/odczytu|Pobiera hello zasobów Centrum IotHub|
|/ iotHubs/zapisu|Utwórz lub zaktualizuj zasób z Centrum IotHub|
|/ iotHubs/Delete|Usuń zasób z Centrum IotHub|
|/iotHubs/listkeys/Action|Pobierz wszystkie klucze Centrum IotHub|
|/iotHubs/exportDevices/Action|Eksportuj urządzeń|
|/iotHubs/importDevices/Action|Importuj urządzeń|
|IotHubs/metricDefinitions/odczytu|Pobiera dostępne metryki hello hello usługi Centrum IotHub|
|/iotHubs/iotHubKeys/listkeys/Action|Pobierz klucz Centrum IotHub hello podanej nazwie|
|/iotHubs/iotHubStats/Read|Uzyskać statystyki Centrum IotHub|
|/iotHubs/quotaMetrics/Read|Pobieraj metryki przydziału|
|/iotHubs/eventHubEndpoints/consumerGroups/Write|Tworzenie grupy konsumentów EventHub|
|/iotHubs/eventHubEndpoints/consumerGroups/Read|Pobierz grupy konsumentów EventHub|
|/iotHubs/eventHubEndpoints/consumerGroups/DELETE|Usuwanie grupy konsumentów EventHub|
|polecenie testall /iotHubs/Routing/Routes/$/działania|Testowa wiadomość przed wszystkie istniejące trasy|
|/iotHubs/Routing/Routes/$ testnew/działania|Testowa wiadomość przed podany test trasy|
|IotHubs/diagnosticSettings/odczytu|Pobiera hello ustawienie diagnostyczne dla zasobu hello|
|/ IotHubs/diagnosticSettings/zapisu|Tworzy lub aktualizuje hello ustawienie diagnostyczne dla zasobu hello|
|/iotHubs/skus/Read|Pobierz prawidłowe jednostki SKU z Centrum IotHub|
|/iotHubs/Jobs/Read|Pobierz zadania szczegóły przesyłane na podany Centrum IotHub|
|/iotHubs/routingEndpointsHealth/Read|Pobiera hello kondycję wszystkich punktów końcowych routingu dla Centrum IotHub|

## <a name="microsoftdevtestlab"></a>Microsoft.DevTestLab

| Operacja | Opis |
|---|---|
|/ Subskrypcji/register/działania|Rejestruje subskrypcję hello|
|/Labs/DELETE|Usuń labs.|
|/Labs/Read|Laboratoria odczytu.|
|/ labs/zapisu|Dodaje lub modyfikuje labs.|
|/Labs/ListVhds/Action|Listy obrazów dysku dostępne na potrzeby tworzenia niestandardowego obrazu.|
|/Labs/GenerateUploadUri/Action|Wygenerować identyfikator URI do przekazywania dysku niestandardowe obrazy tooa laboratorium.|
|/Labs/CreateEnvironment/Action|Tworzenie maszyn wirtualnych w laboratorium.|
|/Labs/ClaimAnyVm/Action|Oświadczenia losowe claimable maszynę wirtualną w laboratorium hello.|
|/Labs/ExportResourceUsage/Action|Eksporty hello laboratorium użycia zasobów na koncie magazynu|
|/Labs/Users/DELETE|Usuń profile użytkowników.|
|/Labs/Users/Read|Przeczytaj profile użytkowników.|
|/Labs/Users/Write|Dodaje lub modyfikuje profile użytkowników.|
|/Labs/Users/secrets/DELETE|Usuwanie kluczy tajnych.|
|/Labs/Users/secrets/Read|Odczyt kluczy tajnych.|
|/Labs/Users/secrets/Write|Dodaje lub modyfikuje kluczy tajnych.|
|/Labs/Users/environments/DELETE|Usuwanie środowiska.|
|/Labs/Users/environments/Read|Przeczytaj środowisk.|
|/Labs/Users/environments/Write|Dodaje lub modyfikuje środowisk.|
|/Labs/Users/Disks/DELETE|Usuń dyski.|
|/Labs/Users/Disks/Read|Przeczytaj dysków.|
|/Labs/Users/Disks/Write|Dodaje lub modyfikuje dysków.|
|/Labs/Users/Disks/Attach/Action|Dołącz i tworzenia dzierżawy hello maszyny wirtualnej toohello dysku hello.|
|/Labs/Users/Disks/detach/Action|Odłącz i dzierżawy hello podział dysku hello dołączone toohello maszyny wirtualnej.|
|/Labs/customImages/DELETE|Usuwanie obrazów niestandardowych.|
|/Labs/customImages/Read|Niestandardowe obrazy.|
|/Labs/customImages/Write|Dodaje lub modyfikuje niestandardowych obrazów.|
|/Labs/serviceRunners/DELETE|Usuń używanych modułów uruchamiających usługi.|
|/Labs/serviceRunners/Read|Przeczytaj używanych modułów uruchamiających usługi.|
|/Labs/serviceRunners/Write|Dodaje lub modyfikuje używanych modułów uruchamiających usługi.|
|/Labs/artifactSources/DELETE|Usuń źródła artefaktu.|
|/Labs/artifactSources/Read|Przeczytaj źródeł artefaktu.|
|/Labs/artifactSources/Write|Dodaje lub modyfikuje źródeł artefaktu.|
|/Labs/artifactSources/artifacts/Read|Przeczytaj artefaktów.|
|/Labs/artifactSources/artifacts/GenerateArmTemplate/Action|Generuje szablonu usługi ARM dla danego artefaktu hello przekazuje hello wymagane pliki tooa magazynu konta i sprawdza poprawność artefaktów hello wygenerowany.|
|/Labs/artifactSources/armTemplates/Read|Przeczytaj szablony Menedżera zasobów platformy azure.|
|/Labs/Costs/Read|Przeczytaj kosztów.|
|/Labs/Costs/Write|Dodaje lub modyfikuje kosztów.|
|/Labs/virtualNetworks/DELETE|Usuwanie sieci wirtualnych.|
|/Labs/virtualNetworks/Read|Przeczytaj sieci wirtualnych.|
|/Labs/virtualNetworks/Write|Dodaje lub modyfikuje sieci wirtualnych.|
|/Labs/Formulas/DELETE|Usuń formuły.|
|/Labs/Formulas/Read|Przeczytaj formuły.|
|/Labs/Formulas/Write|Dodaje lub modyfikuje formuły.|
|/Labs/Schedules/DELETE|Usuń harmonogramów.|
|/Labs/Schedules/Read|Przeczytaj harmonogramów.|
|/Labs/Schedules/Write|Dodaje lub modyfikuje harmonogramów.|
|/Labs/Schedules/EXECUTE/Action|Wykonanie zgodnie z harmonogramem.|
|/Labs/Schedules/ListApplicable/Action|Wyświetla listę wszystkich odpowiednich harmonogramów|
|/Labs/galleryImages/Read|Przeczytaj obrazów w galerii.|
|/Labs/policySets/EvaluatePolicies/Action|Ocenia zasady laboratorium.|
|/Labs/policySets/policies/DELETE|Usuwanie zasad.|
|/Labs/policySets/policies/Read|Przeczytaj zasady.|
|/Labs/policySets/policies/Write|Dodaje lub modyfikuje zasady.|
|/Labs/virtualMachines/DELETE|Usuń maszyny wirtualne.|
|/Labs/virtualMachines/Read|Maszyny wirtualne do odczytu.|
|/Labs/virtualMachines/Write|Dodaje lub modyfikuje maszyny wirtualne.|
|/Labs/virtualMachines/Start/Action|Uruchom maszynę wirtualną.|
|/Labs/virtualMachines/Stop/Action|Zatrzymaj maszynę wirtualną|
|/Labs/virtualMachines/ApplyArtifacts/Action|Zastosuj artefakty toovirtual maszyny.|
|/Labs/virtualMachines/AddDataDisk/Action|Dołącz maszynę toovirtual dysku nowych lub istniejących danych.|
|/Labs/virtualMachines/DetachDataDisk/Action|Odłączyć hello określony dysk z hello maszyny wirtualnej.|
|/Labs/virtualMachines/Claim/Action|Przejmowanie na własność istniejącej maszyny wirtualnej|
|/Labs/virtualMachines/ListApplicableSchedules/Action|Wyświetla listę wszystkich odpowiednich harmonogramów|
|/Labs/virtualMachines/Schedules/DELETE|Usuń harmonogramów.|
|/Labs/virtualMachines/Schedules/Read|Przeczytaj harmonogramów.|
|/Labs/virtualMachines/Schedules/Write|Dodaje lub modyfikuje harmonogramów.|
|/Labs/virtualMachines/Schedules/EXECUTE/Action|Wykonanie zgodnie z harmonogramem.|
|/Labs/notificationChannels/DELETE|Usuń notificationchannels.|
|/Labs/notificationChannels/Read|Przeczytaj notificationchannels.|
|/Labs/notificationChannels/Write|Dodaje lub modyfikuje notificationchannels.|
|/Labs/notificationChannels/Notify/Action|Wyślij powiadomienie tooprovided kanału.|
|/Schedules/DELETE|Usuń harmonogramów.|
|/Schedules/Read|Przeczytaj harmonogramów.|
|/ harmonogramy/zapisu|Dodaje lub modyfikuje harmonogramów.|
|/Schedules/EXECUTE/Action|Wykonanie zgodnie z harmonogramem.|
|/Schedules/Retarget/Action|Aktualizuje zasób docelowy zgodnie z harmonogramem identyfikatora.|
|/Locations/Operations/Read|Operacje odczytu.|

## <a name="microsoftdocumentdb"></a>Microsoft.DocumentDB

| Operacja | Opis |
|---|---|
|/databaseAccountNames/Read|Sprawdza dostępność nazwy.|
|/databaseAccounts/Read|Odczytuje konta bazy danych.|
|/ databaseAccounts/zapisu|Aktualizacja konta bazy danych.|
|/databaseAccounts/listKeys/Action|Listy kluczy konta bazy danych|
|/databaseAccounts/regenerateKey/Action|Obróć klucze konta bazy danych|
|/databaseAccounts/listConnectionStrings/Action|Pobierz hello parametry połączenia dla konta bazy danych|
|/databaseAccounts/changeResourceGroup/Action|Zmiana grupy zasobów dla konta bazy danych|
|/databaseAccounts/failoverPriorityChange/Action|Zmiany priorytetów trybu failover regionów konta bazy danych. Jest to używane tooperform operacji ręcznego przełączania trybu failover|
|/databaseAccounts/DELETE|Usuwa hello konta bazy danych.|
|/databaseAccounts/metricDefinitions/Read|Odczytuje definicje metryk hello konta bazy danych.|
|/databaseAccounts/Metrics/Read|Odczytuje hello bazy danych konta metryki.|
|/databaseAccounts/Usages/Read|Odczytuje hello bazy danych konta użycia.|
|/databaseAccounts/Databases/Collections/metricDefinitions/Read|Odczytuje kolekcję hello definicji metryk.|
|/databaseAccounts/Databases/Collections/Metrics/Read|Odczytuje hello kolekcji metryki.|
|/databaseAccounts/Databases/Collections/Usages/Read|Odczytuje hello użycia kolekcji.|
|/databaseAccounts/Databases/metricDefinitions/Read|Odczytuje definicji metryk hello bazy danych|
|/databaseAccounts/Databases/Metrics/Read|Odczytuje hello metryki bazy danych.|
|/databaseAccounts/Databases/Usages/Read|Odczytuje hello użycia bazy danych.|
|/databaseAccounts/readonlykeys/Read|Odczytuje hello konto bazy danych tylko do odczytu klucze.|

## <a name="microsoftdomainregistration"></a>Microsoft.DomainRegistration

| Operacja | Opis |
|---|---|
|/ generateSsoRequest/działania|Generuje żądanie podpisywania domeny control Center.|
|/ validateDomainRegistrationInformation/działania|Sprawdzanie poprawności obiektu zakupu domeny bez przesyłania|
|/ checkDomainAvailability/działania|Sprawdź, czy domeny jest dostępne do zakupu|
|/ listDomainRecommendations/działania|Pobierz zalecenia domeny listy hello na podstawie słów kluczowych|
|/ register/działania|Rejestrowanie dostawcy zasobów Domains Microsoft hello hello subskrypcji|
|/ domen/odczytu|Pobierz listę hello domen|
|/ domen/zapisu|Dodaj nową domenę lub zaktualizuj istniejącą|
|/ domen/Delete|Usuń istniejącą domenę.|
|/Domains/operationresults/Read|Operacja domeny pobierania|

## <a name="microsoftdynamicslcs"></a>Microsoft.DynamicsLcs

| Operacja | Opis |
|---|---|
|/lcsprojects/Read|Wyświetl projekty Microsoft Dynamics cyklu życia usług, które należą tooa użytkownika|
|/ lcsprojects/zapisu|Tworzenie i aktualizowanie projektów usług Microsoft Dynamics cyklu życia, które należą toohello użytkownika. Można aktualizować tylko hello nazwę i opis właściwości. Nie można zaktualizować subskrypcji Hello i lokalizację skojarzone z projektem powitania po utworzeniu|
|/lcsprojects/DELETE|Usuń projekty Microsoft Dynamics cyklu życia usług, które należą toohello użytkownika|
|/lcsprojects/clouddeployments/Read|Wyświetl Microsoft Dynamics AX 2012 R3 oceny wdrożenia w projekcie Microsoft Dynamics cyklu życia usług, które należy tooa użytkownika|
|/lcsprojects/clouddeployments/Write|Utwórz Microsoft Dynamics AX 2012 R3 oceny wdrożenia w projekcie Microsoft Dynamics cyklu życia usług, które należy tooa użytkownika. Wdrożeń można zarządzać za pomocą portalu zarządzania Azure|
|/lcsprojects/Connectors/Read|Przeczytaj łączniki, które należy tooa usług Microsoft Dynamics cyklu życia projektu|
|/lcsprojects/Connectors/Write|Tworzenie i aktualizowanie łączniki, które należy tooa usług Microsoft Dynamics cyklu życia projektu|

## <a name="microsofteventhub"></a>Microsoft.EventHub

| Operacja | Opis |
|---|---|
|/ checkNameAvailability/działania|Sprawdza dostępność przestrzeni nazw w ramach danej subskrypcji.|
|/ register/działania|Rejestruje subskrypcję dostawcy zasobów EventHub hello hello i umożliwia tworzenie hello EventHub zasobów|
|/ przestrzenie nazw/zapisu|Utwórz zasób Namespace i zaktualizuj jego właściwości. Znaczniki i stan hello Namespace są hello właściwości, które mogą być aktualizowane.|
|/Namespaces/Read|Pobierz listę hello Namespace opis zasobu|
|przestrzenie nazw/Delete|Usuń zasób Namespace|
|/Namespaces/metricDefinitions/Read|Pobierz listę metryki Namespace opisów zasobów|
|/Namespaces/authorizationRules/Read|Pobierz listę hello opis reguły autoryzacji przestrzeni nazw.|
|/Namespaces/authorizationRules/Write|Tworzenie reguł autoryzacji z poziomu Namespace i aktualizowanie jej właściwości. Prawa dostępu reguł autoryzacji Hello, hello podstawowej i dodatkowej klucze mogą być aktualizowane.|
|/Namespaces/authorizationRules/DELETE|Usuń regułę autoryzacji Namespace. Nie można usunąć Hello domyślna reguła autoryzacji Namespace. |
|/Namespaces/authorizationRules/listkeys/Action|Pobierz toohello parametry połączenia hello Namespace|
|/Namespaces/authorizationRules/regenerateKeys/Action|Wygeneruj ponownie hello podstawowej lub pomocniczej klucza toohello zasobów|
|/Namespaces/eventhubs/Write|Tworzenie lub aktualizacja EventHub właściwości.|
|/Namespaces/eventhubs/Read|Pobierz listę opisów zasobów EventHub|
|/Namespaces/eventhubs/DELETE|Operacja toodelete EventHub zasobów|
|/Namespaces/eventHubs/consumergroups/Write|Utwórz lub właściwości grupy konsumentów aktualizacji.|
|/Namespaces/eventHubs/consumergroups/Read|Pobierz listę opisów zasobów grupy konsumentów|
|/Namespaces/eventHubs/consumergroups/DELETE|Operacja toodelete zasobów grupy konsumentów|
|/Namespaces/eventhubs/authorizationRules/Read| Pobierz listę hello EventHub reguł autoryzacji|
|/Namespaces/eventhubs/authorizationRules/Write|Tworzenie reguł autoryzacji EventHub i aktualizowanie jej właściwości. Prawa dostępu reguł autoryzacji Hello, hello podstawowej i dodatkowej klucze mogą być aktualizowane.|
|/Namespaces/eventhubs/authorizationRules/DELETE|Operacja toodelete EventHub reguł autoryzacji|
|/Namespaces/eventhubs/authorizationRules/listkeys/Action|Pobierz hello tooEventHub parametry połączenia|
|/Namespaces/eventhubs/authorizationRules/regenerateKeys/Action|Wygeneruj ponownie hello podstawowej lub pomocniczej klucza toohello zasobów|
|/Namespaces/diagnosticSettings/Read|Pobierz listę Namespace ustawień diagnostycznych zasobu opisów|
|/Namespaces/diagnosticSettings/Write|Pobierz listę Namespace ustawień diagnostycznych zasobu opisów|
|/Namespaces/logDefinitions/Read|Pobierz listę dzienników Namespace opisów zasobów|

## <a name="microsoftfeatures"></a>Microsoft.Features

| Operacja | Opis |
|---|---|
|/Providers/Features/Read|Pobiera hello funkcję subskrypcji danego dostawcy zasobów.|
|/Providers/Features/Register/Action|Rejestruje funkcję subskrypcji hello w danego dostawcy zasobów.|
|/Features/Read|Pobiera funkcje hello subskrypcji.|

## <a name="microsofthdinsight"></a>Microsoft.HDInsight

| Operacja | Opis |
|---|---|
|/ klastrów/zapisu|Utwórz lub zaktualizuj klastra usługi HDInsight|
|/Clusters/Read|Uzyskiwanie szczegółowych informacji dotyczących klastra usługi HDInsight|
|/Clusters/DELETE|Usuwanie klastra usługi HDInsight|
|/Clusters/changerdpsetting/Action|Zmień ustawienie protokołu RDP dla klastra usługi HDInsight|
|/Clusters/Configurations/Action|Zaktualizuj konfigurację klastra usługi HDInsight|
|/Clusters/Configurations/Read|Pobierz konfiguracje klastrów usługi HDInsight|
|/Clusters/Roles/Resize/Action|Zmień rozmiar klastra usługi HDInsight|
|/Locations/Capabilities/Read|Pobrać możliwości subskrypcji|
|/Locations/checkNameAvailability/Read|Sprawdź dostępność nazwy|

## <a name="microsoftimportexport"></a>Microsoft.ImportExport

| Operacja | Opis |
|---|---|
|/ register/działania|Rejestruje hello subskrypcji dla dostawcy zasobów importu/eksportu hello i umożliwia tworzenie hello zadania importu/eksportu.|
|/ zadania/zapisu|Tworzy zadanie o hello określonych parametrów lub zaktualizuj właściwości hello lub tagi dla hello określonego zadania.|
|/Jobs/Read|Pobiera właściwości hello hello określonego zadania lub zwraca hello listy zadań.|
|/Jobs/listBitLockerKeys/Action|Pobiera klucze funkcji BitLocker hello hello określonego zadania.|
|/Jobs/DELETE|Usuwa istniejące zadanie.|
|/Locations/Read|Pobiera właściwości hello hello określonej lokalizacji lub zwraca hello listy lokalizacji.|

## <a name="microsoftinsights"></a>Elemencie Microsoft.Insights

| Operacja | Opis |
|---|---|
|/ Register/działania|Zarejestruj dostawcę usługi insights microsoft hello|
|/ AlertRules/zapisu|Zapisywanie tooan reguła alertu konfiguracji|
|/ AlertRules/usuwania|Usuwanie konfiguracji reguły alertu|
|AlertRules/odczytu|Odczytywanie konfiguracji reguły alertu|
|/ AlertRules/aktywowany/działania|Reguła alertu aktywowany|
|/ AlertRules/rozpoznać/działania|Reguła alertu rozwiązany|
|/ AlertRules/ograniczany/działania|Reguła alertu jest ograniczany.|
|AlertRules/zdarzenia/odczytu|Odczytywanie konfiguracji zdarzenia reguły alertu|
|MetricDefinitions/odczytu|Odczyt definicji metryk|
|/eventtypes/VALUES/Read|Typ zdarzeń zarządzania — odczytaj wartości|
|/eventtypes/digestevents/Read|Typ zdarzeń zarządzania — odczytaj podsumowanie|
|Metryki/odczytu|Odczytać metryki|
|/ LogProfiles/zapisu|Zapisywanie tooa dziennika profilu konfiguracji|
|/ LogProfiles/usuwania|Usuń konfigurację profilów dziennika|
|LogProfiles/odczytu|Profile dziennika odczytu|
|/ AutoscaleSettings/zapisu|Zapisywanie konfiguracji Ustawienia skalowania automatycznego tooan|
|/ AutoscaleSettings/usuwania|Usuwanie konfiguracji ustawienia autoskalowania|
|AutoscaleSettings/odczytu|Odczytywanie konfiguracji ustawienia autoskalowania|
|/ AutoscaleSettings/Scaleup/działania|Autoskalowanie — operacja skalowania w górę|
|/ AutoscaleSettings/Scaledown/działania|Skalowania automatycznego skalowania dół operacji|
|/AutoscaleSettings/Providers/Microsoft.Insights/MetricDefinitions/Read|Odczyt definicji metryk|
|/ ActivityLogAlerts/aktywowany/działania|Działanie dziennika alertów wyzwalanych hello|
|/ DiagnosticSettings/zapisu|Zapisywanie toodiagnostic ustawień konfiguracji|
|/ DiagnosticSettings/usuwania|Usuwanie konfiguracji ustawień diagnostycznych|
|DiagnosticSettings/odczytu|Odczytywanie konfiguracji ustawień diagnostycznych|
|LogDefinitions/odczytu|Odczytaj definicje dzienników|
|/ ExtendedDiagnosticSettings/zapisu|Konfiguracja ustawień diagnostycznych tooextended zapisu|
|/ ExtendedDiagnosticSettings/usuwania|Usuwanie konfiguracji rozszerzonej ustawień diagnostycznych|
|ExtendedDiagnosticSettings/odczytu|Odczytywanie konfiguracji rozszerzonej ustawień diagnostycznych|

## <a name="microsoftkeyvault"></a>Microsoft.KeyVault

| Operacja | Opis |
|---|---|
|/ register/działania|Rejestruje subskrypcję|
|/checkNameAvailability/Read|Sprawdza, czy nazwa magazynu kluczy jest prawidłowa oraz czy została już użyta|
|/vaults/Read|Wyświetlanie właściwości hello magazyn kluczy|
|/ Magazyny/zapisu|Utwórz nowy, klucza hello aktualizacji lub magazynie właściwości istniejący magazyn kluczy|
|/vaults/DELETE|Usuń magazyn kluczy|
|/vaults/Deploy/Action|Umożliwia dostęp do toosecrets w magazynie kluczy, podczas wdrażania zasobów platformy Azure|
|/vaults/secrets/Read|Wyświetl właściwości hello klucz tajny, ale nie jej wartość|
|/vaults/secrets/Write|Utwórz nową wartość hello klucz tajny lub aktualizacji z istniejącym kluczem tajnym|
|/vaults/accessPolicies/Write|Zaktualizuj istniejących zasad dostępu przez scalanie lub wymiana lub Dodaj nowy magazyn tooa zasad dostępu.|
|/deletedVaults/Read|Wyświetl właściwości hello nietrwałego usunięto magazynów kluczy|
|/Locations/operationResults/Read|Sprawdź wynik hello operacji długoterminowym|
|/Locations/deletedVaults/Read|Wyświetlanie właściwości hello nietrwałego usunąć magazyn kluczy|
|/Locations/deletedVaults/PURGE/Action|Przeczyść nietrwałego usunięto magazyn kluczy|

## <a name="microsoftlogic"></a>Microsoft.Logic

| Operacja | Opis |
|---|---|
|/Workflows/Read|Odczytuje hello przepływu pracy.|
|/ przepływy pracy/zapisu|Tworzy lub aktualizuje hello przepływu pracy.|
|/Workflows/DELETE|Usuwa hello przepływu pracy.|
|/Workflows/Run/Action|Uruchamia Uruchom hello przepływu pracy.|
|/Workflows/disable/Action|Wyłącza hello przepływu pracy.|
|/Workflows/enable/Action|Umożliwia hello przepływu pracy.|
|/Workflows/Validate/Action|Weryfikuje hello przepływu pracy.|
|/Workflows/Move/Action|Przenosi przepływu pracy z jego istniejących identyfikator subskrypcji, grupy zasobów i/lub identyfikator nazwy tooa innej subskrypcji, grupy zasobów i/lub nazwę.|
|/Workflows/listSwagger/Action|Pobiera przepływu pracy hello definicji struktury swagger.|
|/Workflows/regenerateAccessKey/Action|Ponowne wygenerowanie klucza kluczy tajnych hello dostępu.|
|/Workflows/listCallbackUrl/Action|Pobiera adres URL wywołania zwrotnego hello przepływu pracy.|
|/Workflows/Versions/Read|Odczytuje hello wersja przepływu pracy.|
|/Workflows/Versions/Triggers/listCallbackUrl/Action|Pobiera adres URL wywołania zwrotnego hello wyzwalacza.|
|przepływy pracy/uruchamia/Odczyt|Odczytuje hello przepływu pracy Uruchom.|
|/Workflows/runs/Cancel/Action|Anuluje hello uruchomienia przepływu pracy.|
|/Workflows/runs/Actions/Read|Odczytuje hello przepływu pracy akcji.|
|/Workflows/runs/Operations/Read|Odczytuje hello przepływu pracy stan operacji.|
|/Workflows/Triggers/Read|Odczytuje hello wyzwalacza.|
|/Workflows/Triggers/Run/Action|Wykonuje hello wyzwalacza.|
|/Workflows/Triggers/listCallbackUrl/Action|Pobiera adres URL wywołania zwrotnego hello wyzwalacza.|
|/Workflows/Triggers/histories/Read|Odczytuje hello wyzwalacza historii.|
|/Workflows/Triggers/histories/resubmit/Action|Przesyła ponownie hello wyzwalacz przepływu pracy.|
|/Workflows/accessKeys/Read|Odczytuje hello klucz dostępu.|
|/Workflows/accessKeys/Write|Tworzy lub aktualizuje hello klucz dostępu.|
|/Workflows/accessKeys/DELETE|Usuwa hello klucz dostępu.|
|/Workflows/accessKeys/list/Action|Wyświetla listę kluczy kluczy tajnych hello dostępu.|
|/Workflows/accessKeys/regenerate/Action|Ponowne wygenerowanie klucza kluczy tajnych hello dostępu.|
|/Locations/Workflows/Validate/Action|Weryfikuje hello przepływu pracy.|

## <a name="microsoftmachinelearning"></a>Microsoft.MachineLearning

| Operacja | Opis |
|---|---|
|/ register/działania|Rejestruje subskrypcję hello hello machine learning dostawcy zasobów usługi sieci web i umożliwia tworzenie hello usług sieci web.|
|/ usług sieci Web/działania|Utwórz regionalnych właściwości obsługiwanych regionów usługi sieci Web|
|/commitmentPlans/Read|Przeczytaj maszyn zobowiązań Plan nauki|
|/ commitmentPlans/zapisu|Utwórz lub zaktualizuj żadnych zobowiązań Plan nauki maszyny|
|/commitmentPlans/DELETE|Usuń wszystkie maszyny zobowiązań Plan nauki|
|/commitmentPlans/JOIN/Action|Dołącz do dowolnej maszyny zobowiązań Plan nauki|
|/commitmentPlans/commitmentAssociations/Read|Przeczytaj maszyn zobowiązań skojarzenia Plan nauki|
|/commitmentPlans/commitmentAssociations/Move/Action|Przenieś wszystkie Machine Learning skojarzenia planu zobowiązań|
|Obszary robocze/odczytu|Wszelkie Machine Learning obszaru roboczego do odczytu|
|/ Workspaces/zapisu|Utwórz lub zaktualizuj wszystkie Machine Learning obszaru roboczego|
|/ Workspaces/usuwania|Usuń wszelkie Machine Learning obszaru roboczego|
|/ Workspaces/listworkspacekeys/działania|Lista kluczy dla obszaru roboczego Machine Learning|
|/ Workspaces/resyncstoragekeys/działania|Zsynchronizowanie klucze konta magazynu skonfigurowanego dla obszaru roboczego Machine Learning|
|/webServices/Read|Usługi sieci Web Machine Learning do odczytu|
|/ usług sieci Web/zapisu|Utwórz lub zaktualizuj usługi sieci Web Machine Learning|
|/webServices/DELETE|Usuń usługi sieci Web Machine Learning|

## <a name="microsoftmarketplaceordering"></a>Microsoft.MarketplaceOrdering

| Operacja | Opis |
|---|---|
|/agreements/offers/plans/Read|Zwraca umowę dla elementu danej witryny marketplace|
|/agreements/offers/plans/sign/Action|Podpisać umowę dla elementu danej witryny marketplace|
|/agreements/offers/plans/Cancel/Action|Anuluj umowę dla elementu danej witryny marketplace|

## <a name="microsoftmedia"></a>Microsoft.Media

| Operacja | Opis |
|---|---|
|/mediaservices/Read||
|/ mediaservices/zapisu||
|/mediaservices/DELETE||
|/mediaservices/regenerateKey/Action||
|/mediaservices/listKeys/Action||
|/mediaservices/syncStorageKeys/Action||

## <a name="microsoftnetwork"></a>Microsoft.Network

| Operacja | Opis |
|---|---|
|/ register/działania|Rejestruje subskrypcję hello|
|/ unregister/działania|Wyrejestrowuje hello subskrypcji|
|/ checkTrafficManagerNameAvailability/działania|Sprawdza dostępność hello nazwy DNS względem usługi Traffic Manager.|
|/dnszones/Read|Pobierz strefę DNS hello, w formacie JSON. Witaj właściwości strefy obejmują tag, etag, numberOfRecordSets i maxNumberOfRecordSets. Należy pamiętać, że to polecenie nie pobiera hello zestawów rekordów znajdujących się w strefie hello.|
|/ dnszones/zapisu|Utwórz lub zaktualizuj strefę DNS w ramach grupy zasobów.  Używane tooupdate hello tagów w zasobie strefy DNS. Należy pamiętać, że to polecenie nie może być używane zestawów rekordów toocreate lub aktualizacji w strefie hello.|
|/dnszones/DELETE|Usuń strefę DNS hello, w formacie JSON. Witaj właściwości strefy obejmują tag, etag, numberOfRecordSets i maxNumberOfRecordSets.|
|/dnszones/MX/Read|Pobierz hello zestaw rekordów typu "MX" w formacie JSON. Hello zestaw rekordów zawiera listę rekordów, a także hello TTL, znaczników i etag.|
|/dnszones/MX/Write|Utwórz lub zaktualizuj zestaw rekordów typu "MX" w strefie DNS. rekordy Hello określone spowoduje zastąpienie hello bieżące rekordy w zestawie rekordów hello.|
|/dnszones/MX/DELETE|Usuń zestaw rekordów hello o danej nazwie i typu "MX" ze strefy DNS.|
|/dnszones/NS/Read|Pobiera zestaw rekordów DNS typu NS|
|/dnszones/NS/Write|Tworzy lub aktualizuje zestaw rekordów DNS typu NS|
|/dnszones/NS/DELETE|Usuwa zestaw rekordów DNS hello typu NS|
|/dnszones/AAAA/Read|Pobierz hello zestaw rekordów typu "AAAA" w formacie JSON. Hello zestaw rekordów zawiera listę rekordów, a także hello TTL, znaczników i etag.|
|/dnszones/AAAA/Write|Utwórz lub zaktualizuj zestaw rekordów typu "AAAA" w strefie DNS. rekordy Hello określone spowoduje zastąpienie hello bieżące rekordy w zestawie rekordów hello.|
|/dnszones/AAAA/DELETE|Usuń zestaw rekordów hello o danej nazwie i typu "AAAA" ze strefy DNS.|
|/dnszones/CNAME/Read|Pobierz hello zestaw rekordów typu "CNAME" w formacie JSON. zestaw rekordów Hello zawiera hello TTL, tag i etag.|
|/dnszones/CNAME/Write|Utwórz lub zaktualizuj zestaw rekordów typu "CNAME" w strefie DNS. rekordy Hello określone spowoduje zastąpienie hello bieżące rekordy w zestawie rekordów hello.|
|/dnszones/CNAME/DELETE|Usuń zestaw rekordów hello o danej nazwie i typu "CNAME" ze strefy DNS.|
|/dnszones/SOA/Read|Pobiera zestaw rekordów DNS typu SOA|
|/dnszones/SOA/Write|Tworzy lub aktualizuje zestaw rekordów DNS typu SOA|
|/dnszones/SRV/Read|Pobierz hello zestaw rekordów typu "SRV" w formacie JSON. Hello zestaw rekordów zawiera listę rekordów, a także hello TTL, znaczników i etag.|
|/dnszones/SRV/Write|Utwórz lub zaktualizuj zestaw rekordów typu SRV|
|/dnszones/SRV/DELETE|Usuń zestaw rekordów hello o danej nazwie i typu "SRV" ze strefy DNS.|
|/dnszones/PTR/Read|Pobierz hello zestaw rekordów typu "PTR" w formacie JSON. Hello zestaw rekordów zawiera listę rekordów, a także hello TTL, znaczników i etag.|
|/dnszones/PTR/Write|Utwórz lub zaktualizuj zestaw rekordów typu "PTR" w strefie DNS. rekordy Hello określone spowoduje zastąpienie hello bieżące rekordy w zestawie rekordów hello.|
|/dnszones/PTR/DELETE|Usuń zestaw rekordów hello o danej nazwie i typu "PTR" ze strefy DNS.|
|/dnszones/A/Read|Pobierz hello zestaw rekordów typu "A", w formacie JSON. Hello zestaw rekordów zawiera listę rekordów, a także hello TTL, znaczników i etag.|
|/dnszones/A/Write|Utwórz lub zaktualizuj zestaw rekordów typu "A" w strefie DNS. rekordy Hello określone spowoduje zastąpienie hello bieżące rekordy w zestawie rekordów hello.|
|/dnszones/A/DELETE|Usuń zestaw rekordów hello o danej nazwie i typu "A" ze strefy DNS.|
|/dnszones/txt/Read|Pobierz hello zestaw rekordów typu "TXT" w formacie JSON. Hello zestaw rekordów zawiera listę rekordów, a także hello TTL, znaczników i etag.|
|/dnszones/txt/Write|Utwórz lub zaktualizuj zestaw rekordów typu "TXT" w strefie DNS. rekordy Hello określone spowoduje zastąpienie hello bieżące rekordy w zestawie rekordów hello.|
|/dnszones/txt/DELETE|Usuń zestaw rekordów hello o danej nazwie i typu "TXT" ze strefy DNS.|
|/dnszones/Recordsets/Read|Pobiera różnych typów zestawów rekordów DNS|
|/networkInterfaces/Read|Pobiera definicję interfejsu sieciowego. |
|/ Networkinterface/zapisu|Tworzy interfejs sieciowy lub aktualizuje istniejący interfejs sieciowy. |
|/networkInterfaces/JOIN/Action|Tworzy sprzężenie tooa interfejsu sieciowego maszyny wirtualnej|
|/networkInterfaces/DELETE|Usuwa interfejs sieciowy|
|/networkInterfaces/effectiveRouteTable/Action|Pobierz tabelę tras skonfigurowane dla interfejsu sieci hello maszyny wirtualnej|
|/networkInterfaces/effectiveNetworkSecurityGroups/Action|Pobierz grup zabezpieczeń sieci skonfigurowane w sieci interfejsu z hello maszyny wirtualnej|
|/networkInterfaces/loadBalancers/Read|Pobiera wszystkie hello usług równoważenia obciążenia interfejsu sieciowego hello jest częścią|
|/networkInterfaces/ipconfigurations/Read|Pobiera definicję konfiguracji adresu ip interfejsu sieciowego. |
|/publicIPAddresses/Read|Pobiera definicję adres publiczny adres ip.|
|/ elementów Publicipaddress/zapisu|Tworzy publiczny adres Ip lub aktualizuje istniejący publiczny adres Ip. |
|/publicIPAddresses/DELETE|Usuwa publiczny adres Ip.|
|/publicIPAddresses/JOIN/Action|Dołącza do publicznego adresu ip|
|/routeFilters/Read|Pobiera definicję filtru tras|
|/routeFilters/JOIN/Action|Dołącza filtr tras|
|/routeFilters/DELETE|Usuwa definicję filtru tras|
|/ routeFilters/zapisu|Tworzy filtr tras lub aktualizuje istniejący filtr tras|
|/routeFilters/Rules/Read|Pobiera definicję reguły filtru trasy|
|/routeFilters/Rules/Write|Tworzy regułę filtru tras lub aktualizuje istniejącą regułę filtru trasy|
|/routeFilters/Rules/DELETE|Usuwa definicję reguły filtru trasy|
|/networkWatchers/Read|Pobierz definicję obserwatora sieciowego hello|
|/ networkWatchers/zapisu|Tworzy obserwatora sieciowego lub aktualizuje istniejącą obserwatora sieciowego|
|/networkWatchers/DELETE|Usuwa obserwatora sieciowego|
|/networkWatchers/configureFlowLog/Action|Konfiguruje przepływu rejestrowanie dla zasobu docelowego.|
|/networkWatchers/ipFlowVerify/Action|Zwraca czy pakietów hello jest dozwolony lub odmowa tooor danego przeznaczenia.|
|/networkWatchers/nextHop/Action|Określony obiekt docelowy oraz docelowy adres IP zwracany typ następnego przeskoku hello i dalej nadzieję, że adres IP.|
|/networkWatchers/queryFlowLogStatus/Action|Pobiera stan hello przepływu rejestrowania w zasobie.|
|/networkWatchers/queryTroubleshootResult/Action|Pobiera hello rozwiązywania problemów w wyniku hello wcześniej uruchomione lub uruchomiona Rozwiązywanie problemów z operacji.|
|/networkWatchers/securityGroupView/Action|Wyświetl skonfigurowane hello i reguły grupy zabezpieczeń sieci skuteczne zastosowane na maszynie Wirtualnej.|
|/networkWatchers/Topology/Action|Pobiera widok poziomu sieci, zasobów i ich relacje w grupie zasobów.|
|/networkWatchers/Troubleshoot/Action|Uruchamia Rozwiązywanie problemów w zasobie sieci na platformie Azure.|
|/networkWatchers/packetCaptures/queryStatus/Action|Pobiera informacje o właściwościach i stan zasobu przechwytywania pakietów.|
|/networkWatchers/packetCaptures/Stop/Action|Zatrzymaj hello, w którym działa sesja przechwytywania pakietów.|
|/networkWatchers/packetCaptures/Read|Pobierz definicję przechwytywania pakietów hello|
|/networkWatchers/packetCaptures/Write|Tworzy przechwytywania pakietów|
|/networkWatchers/packetCaptures/DELETE|Usuwa przechwytywania pakietów|
|/loadBalancers/Read|Pobiera definicję modułu równoważenia obciążenia|
|/ loadBalancers/zapisu|Tworzy moduł równoważenia obciążenia lub aktualizuje istniejący moduł równoważenia obciążenia|
|/loadBalancers/DELETE|Usuwa usługę równoważenia obciążenia|
|/loadBalancers/networkInterfaces/Read|Pobiera odwołania do interfejsów sieciowych hello tooall należących do modułu równoważenia obciążenia|
|/loadBalancers/loadBalancingRules/Read|Pobiera definicję modułu równoważenia obciążenia obciążenia równoważenia reguły|
|/loadBalancers/backendAddressPools/Read|Pobiera definicję puli adresów zaplecza modułu równoważenia obciążenia|
|/loadBalancers/backendAddressPools/JOIN/Action|Dołącza do puli adresów zaplecza modułu równoważenia obciążenia|
|/loadBalancers/inboundNatPools/Read|Pobiera moduł równoważenia obciążenia ruchu przychodzącego definicję puli translacji nat|
|/loadBalancers/inboundNatPools/JOIN/Action|Tworzy sprzężenie modułu równoważenia obciążenia ruchu przychodzącego pulę translacji nat|
|/loadBalancers/inboundNatRules/Read|Pobiera moduł równoważenia obciążenia definicję przychodzącej reguły nat|
|/loadBalancers/inboundNatRules/Write|Tworzy regułę nat dla ruchu przychodzącego modułu równoważenia obciążenia lub aktualizuje istniejącą regułę nat dla ruchu przychodzącego modułu równoważenia obciążenia|
|/loadBalancers/inboundNatRules/DELETE|Usuwa regułę nat dla ruchu przychodzącego modułu równoważenia obciążenia|
|/loadBalancers/inboundNatRules/JOIN/Action|Tworzy sprzężenie reguły nat dla ruchu przychodzącego modułu równoważenia obciążenia|
|/loadBalancers/outboundNatRules/Read|Pobiera definicję reguły nat ruchu wychodzącego modułu równoważenia obciążenia|
|/loadBalancers/probes/Read|Pobiera sondę modułu równoważenia obciążenia|
|/loadBalancers/virtualMachines/Read|Pobiera odwołania do maszyn wirtualnych hello tooall w ramach usługi równoważenia obciążenia|
|/loadBalancers/frontendIPConfigurations/Read|Pobiera definicję konfiguracji IP frontonu modułu równoważenia obciążenia|
|/trafficManagerGeographicHierarchies/Read|Pobiera hello hierarchii Geographic Traffic Manager zawierający regionów, które mogą być używane z hello metody routingu ruchu geograficzne|
|/bgpServiceCommunities/Read|Pobierz społeczności usługi protokołu Bgp|
|/applicationGatewayAvailableWafRuleSets/Read|Pobiera bramę aplikacji, ustawia dostępne reguły zapory aplikacji sieci Web|
|/virtualNetworks/Read|Pobierz definicję sieci wirtualnej hello|
|/ virtualNetworks/zapisu|Tworzy sieć wirtualną lub aktualizuje istniejącą sieć wirtualną|
|/virtualNetworks/DELETE|Usuwa sieci wirtualnej|
|/virtualNetworks/peer/Action|Równorzędnymi użytkownikami sieci wirtualnej z inną siecią wirtualną|
|/virtualNetworks/virtualNetworkPeerings/Read|Pobiera definicję sieci wirtualnej komunikacji równorzędnej|
|/virtualNetworks/virtualNetworkPeerings/Write|Tworzy element równorzędny sieci wirtualnej lub aktualizuje istniejące sieci wirtualnej komunikacji równorzędnej|
|/virtualNetworks/virtualNetworkPeerings/DELETE|Usuwa element równorzędny sieci wirtualnej|
|/virtualNetworks/Subnets/Read|Pobiera definicję podsieci sieci wirtualnej|
|/virtualNetworks/Subnets/Write|Tworzy podsieć sieci wirtualnej lub aktualizuje istniejącą podsieć sieci wirtualnej|
|/virtualNetworks/Subnets/DELETE|Usuwa podsieć sieci wirtualnej|
|/virtualNetworks/Subnets/JOIN/Action|Tworzy sprzężenie sieci wirtualnej|
|/virtualNetworks/Subnets/joinViaServiceTunnel/Action|Tworzy sprzężenie zasobów, takich jak konta magazynu lub SQL bazy danych tooa usługi tunelowania włączone podsieci.|
|/virtualNetworks/Subnets/virtualMachines/Read|Pobiera odwołania do maszyn wirtualnych hello tooall w podsieci sieci wirtualnej|
|/virtualNetworks/checkIpAddressAvailability/Read|Sprawdź, czy adres Ip jest dostępna na powitania określonej sieci wirtualnej|
|/virtualNetworks/virtualMachines/Read|Pobiera odwołania do maszyn wirtualnych hello tooall w sieci wirtualnej|
|/expressRouteServiceProviders/Read|Pobiera dostawców usługi Expressroute|
|/dnsoperationresults/Read|Pobiera wyniki operacji DNS|
|/localnetworkgateways/Read|Pobiera LocalNetworkGateway|
|/ localnetworkgateways/zapisu|Tworzy lub aktualizuje istniejące LocalNetworkGateway|
|/localnetworkgateways/DELETE|Usuwa LocalNetworkGateway|
|/trafficManagerProfiles/Read|Pobierz konfigurację profilu Menedżera ruchu hello. W tym ustawienia DNS, ustawienia kierowania ruchu, ustawienia monitorowania punktu końcowego i hello listę punktów końcowych kierowanych przez ten profil Menedżera ruchu.|
|/ trafficManagerProfiles/zapisu|Tworzenie profilu Menedżera ruchu lub modyfikowanie konfiguracji hello istniejącego profilu Menedżera ruchu. Dotyczy to również włączenia lub wyłączenia profilu i modyfikowanie ustawień DNS, ustawienia kierowania ruchu lub ustawień monitorowania dla punktu końcowego. Punkty końcowe kierowane przez profil Menedżera ruchu hello może dodać, usunąć, włączona lub wyłączona.|
|/trafficManagerProfiles/DELETE|Usuwanie profilu Menedżera ruchu hello. Wszystkie ustawienia skojarzone z hello profilu Menedżera ruchu zostaną utracone i hello profilu nie można go już używać tooroute ruchu.|
|/dnsoperationstatuses/Read|Pobiera stan operacji DNS |
|/Operations/Read|Pobiera dostępne operacje|
|/expressRouteCircuits/Read|Pobierz ExpressRouteCircuit|
|/ expressRouteCircuits/zapisu|Tworzy lub aktualizuje istniejące ExpressRouteCircuit|
|/expressRouteCircuits/DELETE|Usuwa ExpressRouteCircuit|
|/expressRouteCircuits/stats/Read|Pobiera stan ExpressRouteCircuit|
|/expressRouteCircuits/peerings/Read|Pobiera ExpressRouteCircuit komunikacji równorzędnej|
|/expressRouteCircuits/peerings/Write|Tworzy lub aktualizuje istniejącą ExpressRouteCircuit komunikacji równorzędnej|
|/expressRouteCircuits/peerings/DELETE|Usuwa ExpressRouteCircuit komunikacji równorzędnej|
|/expressRouteCircuits/peerings/arpTables/Action|Pobiera ExpressRouteCircuit ArpTable komunikacji równorzędnej|
|/expressRouteCircuits/peerings/routeTables/Action|Pobiera stan równorzędna ExpressRouteCircuit|
|/expressRouteCircuits/komunikacji równorzędnych /<br>routeTablesSummary/działania|Pobiera ExpressRouteCircuit równorzędna stan podsumowanie|
|/expressRouteCircuits/peerings/stats/Read|Pobiera ExpressRouteCircuit równorzędna Stat|
|/expressRouteCircuits/authorizations/Read|Pobiera autoryzacji ExpressRouteCircuit|
|/expressRouteCircuits/authorizations/Write|Tworzy lub aktualizuje istniejącą autoryzacji ExpressRouteCircuit|
|/expressRouteCircuits/authorizations/DELETE|Usuwa ExpressRouteCircuit autoryzacji|
|/Connections/Read|Pobiera element VirtualNetworkGatewayConnection|
|/ połączeń/zapisu|Tworzy lub aktualizuje istniejący element VirtualNetworkGatewayConnection|
|/Connections/DELETE|Usuwa element VirtualNetworkGatewayConnection|
|/Connections/sharedKey/Read|Pobiera element VirtualNetworkGatewayConnection SharedKey|
|/Connections/sharedKey/Write|Tworzy lub aktualizuje istniejącą SharedKey element VirtualNetworkGatewayConnection|
|/networkSecurityGroups/Read|Pobiera definicję grupy zabezpieczeń sieci|
|/ Networksecuritygroup/zapisu|Tworzy sieciową grupę zabezpieczeń lub aktualizuje istniejącą sieciową grupę zabezpieczeń|
|/networkSecurityGroups/DELETE|Usuwa sieciową grupę zabezpieczeń|
|/networkSecurityGroups/JOIN/Action|Dołącza do sieciowej grupy zabezpieczeń|
|/networkSecurityGroups/defaultSecurityRules/Read|Pobiera domyślną definicję reguły zabezpieczeń|
|/networkSecurityGroups/securityRules/Read|Pobiera definicję reguły zabezpieczeń|
|/networkSecurityGroups/securityRules/Write|Tworzy regułę zabezpieczeń lub aktualizuje istniejącą regułę zabezpieczeń|
|/networkSecurityGroups/securityRules/DELETE|Usuwa regułę zabezpieczeń|
|/applicationGateways/Read|Pobiera bramę aplikacji|
|/ applicationGateways/zapisu|Tworzy bramę aplikacji lub aktualizuje istniejącą bramę aplikacji|
|/applicationGateways/DELETE|Usuwa bramę aplikacji|
|/applicationGateways/backendhealth/Action|Pobiera kondycji zaplecza bramy aplikacji|
|/applicationGateways/Start/Action|Uruchamia bramy aplikacji|
|/applicationGateways/Stop/Action|Zatrzymuje bramy aplikacji|
|/applicationGateways/backendAddressPools/JOIN/Action|Dołącza do puli adresów zaplecza bramy aplikacji|
|/routeTables/Read|Pobiera definicję tabeli tras|
|/ routeTables/zapisu|Tworzy tabelę tras lub aktualizuje istniejącą tabelę tras|
|/routeTables/DELETE|Usuwa definicję tabeli tras|
|/routeTables/JOIN/Action|Tworzy sprzężenie tabeli tras|
|/routeTables/Routes/Read|Pobiera definicję trasy|
|/routeTables/Routes/Write|Tworzy trasę lub aktualizuje istniejącą trasę|
|/routeTables/Routes/DELETE|Usuwa definicję trasy|
|/Locations/operationResults/Read|Pobiera wynik operacji asynchronicznej POST lub operacja usuwania|
|/Locations/checkDnsNameAvailability/Read|Sprawdza, czy etykieta dns jest dostępna na powitania określonej lokalizacji|
|/Locations/Usages/Read|Pobiera metryki użycia zasobów hello|
|/Locations/Operations/Read|Pobiera zasób operacji reprezentujący stan operacji asynchronicznej|

## <a name="microsoftnotificationhubs"></a>Microsoft.NotificationHubs

| Operacja | Opis |
|---|---|
|/ register/działania|Rejestruje subskrypcję dostawcy zasobów NotifciationHubs hello hello i umożliwia tworzenie hello obszary nazw i NotificationHubs|
|/ CheckNamespaceAvailability/działania|Sprawdza, czy podana nazwa zasobu Namespace jest dostępne w ramach hello NotificationHub usługi.|
|Przestrzenie nazw/zapisu|Utwórz zasób Namespace i zaktualizuj jego właściwości. Znaczniki i stan hello Namespace są hello właściwości, które mogą być aktualizowane.|
|Przestrzenie nazw/odczytu|Pobierz listę hello Namespace opis zasobu|
|/ Przestrzenie nazw/usuwania|Usuń zasób Namespace|
|/ Przestrzenie nazw/authorizationRules/działania|Pobierz listę hello opis reguły autoryzacji przestrzeni nazw.|
|/ Przestrzenie nazw/CheckNotificationHubAvailability/działania|Sprawdza, czy dana nazwa usługi NotificationHub jest dostępna w przestrzeni nazw.|
|Przestrzenie nazw/authorizationRules/zapisu|Tworzenie reguł autoryzacji z poziomu Namespace i aktualizowanie jej właściwości. Prawa dostępu reguł autoryzacji Hello, hello podstawowej i dodatkowej klucze mogą być aktualizowane.|
|Przestrzenie nazw/authorizationRules/odczytu|Pobierz listę hello opis reguły autoryzacji przestrzeni nazw.|
|/ Przestrzenie nazw/authorizationRules/usuwania|Usuń regułę autoryzacji Namespace. Nie można usunąć Hello domyślna reguła autoryzacji Namespace. |
|/ Przestrzenie nazw/authorizationRules/listkeys/działania|Pobierz toohello parametry połączenia hello Namespace|
|/ Przestrzenie nazw/authorizationRules/regenerateKeys/działania|Namespace autoryzacji reguły ponownie wygenerować podstawowy/klucz pomocniczy, określ hello toobe ponownego wygenerowania klucza|
|Przestrzenie nazw/NotificationHubs/zapisu|Tworzenie Centrum powiadomień i aktualizowanie jej właściwości. Jego właściwości obejmują głównie poświadczeń systemu powiadomień platformy. Reguły autoryzacji i czas wygaśnięcia|
|Przestrzenie nazw/NotificationHubs/odczytu|Pobierz listę opisów zasobów centrum powiadomień|
|/ Przestrzenie nazw/NotificationHubs/usuwania|Usuń zasób Centrum powiadomień|
|/ Przestrzenie nazw/NotificationHubs/authorizationRules/działania|Pobierz listę hello reguły autoryzacji Centrum powiadomień|
|/ Przestrzenie nazw/NotificationHubs/pnsCredentials/działania|Pobierz wszystkie poświadczenia systemu powiadomień platformy Centrum powiadomień. Obejmuje to poświadczenia usługi WNS, MPNS, APNS, usługi GCM i Baidu|
|/ Przestrzenie nazw/NotificationHubs/debugSend/działania|Wyślij testowe powiadomienie wypychane.|
|Przestrzenie nazw/NotificationHubs/metricDefinitions/odczytu|Pobierz listę metryki Namespace opisów zasobów|
|/Namespaces/NotificationHubs /<br>authorizationRules/zapisu|Tworzenie reguł autoryzacji Centrum powiadomień i aktualizowanie jej właściwości. Prawa dostępu reguł autoryzacji Hello, hello podstawowej i dodatkowej klucze mogą być aktualizowane.|
|/Namespaces/NotificationHubs /<br>authorizationRules/Odczyt|Pobierz listę hello reguły autoryzacji Centrum powiadomień|
|/Namespaces/NotificationHubs /<br>authorizationRules/usuwania|Usuń reguły autoryzacji centrum powiadomień|
|/Namespaces/NotificationHubs /<br>Akcja authorizationRules/listkeys|Pobierz hello toohello parametry połączenia Centrum powiadomień|
|/Namespaces/NotificationHubs /<br>Akcja authorizationRules/regenerateKeys|Powiadomienia Centrum autoryzacji reguły ponownie wygenerować podstawowy/klucz pomocniczy, określ hello toobe ponownego wygenerowania klucza|

## <a name="microsoftoperationalinsights"></a>Microsoft.OperationalInsights

| Operacja | Opis |
|---|---|
|/ register/działania|Zarejestruj dostawcę zasobów tooa subskrypcji.|
|/linkTargets/Read|Wyświetla listę istniejących kont, które nie są skojarzone z subskrypcją platformy Azure. toolink ten obszar roboczy tooa subskrypcji platformy Azure, użyj identyfikatora klienta zwracane przez tę operację we właściwości identyfikatora klienta hello hello operacji Utwórz obszar roboczy.|
|/ workspaces/zapisu|Tworzy nowy obszar roboczy lub istniejący obszar roboczy łącza tooan zapewniając hello identyfikator klienta z istniejącym obszarem roboczym hello.|
|/workspaces/Read|Pobiera istniejący obszar roboczy|
|/workspaces/DELETE|Usuwa obszaru roboczego. Jeśli hello obszaru roboczego został połączony tooan istniejący obszar roboczy w czasie tworzenia następnie hello obszar roboczy był połączony toois nie został usunięty.|
|/workspaces/generateregistrationcertificate/Action|Generuje certyfikatu rejestracji dla hello obszaru roboczego. Ten certyfikat jest używany tooconnect Microsoft System Center Operations Manager toohello roboczym.|
|/workspaces/sharedKeys/Action|Pobiera klucze hello udostępnionych hello obszaru roboczego. Te klucze są używane tooconnect Microsoft Operational Insights agentów toohello roboczym.|
|/workspaces/Search/Action|Wykonuje zapytanie wyszukiwania|
|/workspaces/Datasources/Read|Pobierz źródeł danych w obszarze roboczym.|
|/workspaces/Datasources/Write|Utwórz/Aktualizuj źródeł danych w obszarze roboczym.|
|/workspaces/Datasources/DELETE|Usuwanie źródeł danych w obszarze roboczym.|
|/workspaces/managementGroups/Read|Pobiera nazwy hello i metadanych dla roboczego toothis podłączonej grupy zarządzania programu System Center Operations Manager.|
|/workspaces/Schema/Read|Pobiera schematu wyszukiwania hello hello obszaru roboczego.  Schematu wyszukiwania zawiera pola hello widoczne i ich typów.|
|/workspaces/Usages/Read|Pobiera dane użycia dla obszaru roboczego, w tym hello ilość odczytanych przez hello obszar roboczy danych.|
|/workspaces/intelligencepacks/Read|Wyświetla listę wszystkich pakietów analizy, które są widoczne dla danego worksapce oraz ich pakiet hello jest włączone lub wyłączone dla tego obszaru roboczego.|
|/workspaces/intelligencepacks/enable/Action|Włącza pakiet analizy dla danego obszaru roboczego.|
|/workspaces/intelligencepacks/disable/Action|Wyłącza pakietu intelligence pack dla danego obszaru roboczego.|
|/workspaces/sharedKeys/Read|Pobiera klucze hello udostępnionych hello obszaru roboczego. Te klucze są używane tooconnect Microsoft Operational Insights agentów toohello roboczym.|
|/workspaces/savedSearches/Read|Pobiera zapytanie zapisanego wyszukiwania|
|/workspaces/savedSearches/Write|Tworzy zapytanie zapisanego wyszukiwania|
|/workspaces/savedSearches/DELETE|Usuwa kwerendę zapisanego wyszukiwania|
|/workspaces/storageinsightconfigs/Write|Tworzy nową konfigurację magazynu. Te konfiguracje są używane toopull danych z lokalizacji w istniejącego konta magazynu.|
|/workspaces/storageinsightconfigs/Read|Pobiera konfiguracji magazynu.|
|/workspaces/storageinsightconfigs/DELETE|Usuwa konfiguracji magazynu. Przestanie Microsoft Operational Insights odczytywanie danych z hello konta magazynu.|
|/workspaces/configurationScopes/Read|Pobierz konfigurację zakresu|
|/workspaces/configurationScopes/Write|Ustawianie zakresu konfiguracji|
|/workspaces/configurationScopes/DELETE|Usuwanie konfiguracji zakresu|

## <a name="microsoftoperationsmanagement"></a>Microsoft.OperationsManagement

| Operacja | Opis |
|---|---|
|/ register/działania|Zarejestruj dostawcę zasobów tooa subskrypcji.|
|/ rozwiązań/zapisu|Utwórz nowe rozwiązanie OMS|
|/Solutions/Read|Pobierz Kończenie rozwiązania OMS|
|/Solutions/DELETE|Usuń istniejące rozwiązanie OMS|

## <a name="microsoftrecoveryservices"></a>Microsoft.RecoveryServices

| Operacja | Opis |
|---|---|
|/ Magazyny/backupJobsExport/działania|Eksportowanie zadań|
|/ Magazyny/zapisu|Operacja Utwórz magazyn tworzy zasób platformy Azure typu „magazyn”|
|Magazyny/odczytu|Witaj operacji Get magazynu pobiera obiekt reprezentujący hello zasobów platformy Azure typu "magazynu"|
|/ Magazyny/usuwania|Witaj usunąć magazyn operacji usunięcia Witaj określony zasobów platformy Azure typu "magazynu"|
|Magazyny/refreshContainers/odczytu|Odświeża listę kontenera hello|
|Magazyny/backupJobsExport/operationResults/odczytu|Witaj zwraca wynik eksportowania zadania działania.|
|Magazyny/backupOperationResults/odczytu|Zwraca wynik operacji tworzenia kopii zapasowej magazynu usług Recovery Services.|
|Magazyny/monitoringAlerts/odczytu|Pobiera hello alertów dla magazynu usług odzyskiwania hello.|
|/Vaults/monitoringAlerts / {uniqueAlertId} / Odczyt|Pobiera szczegóły hello hello alertu.|
|Magazyny/backupSecurityPIN/odczytu|Zwraca zabezpieczający numer PIN informacji odzyskiwania usług magazynu.|
|/vaults/replicationEvents/Read|Przeczytaj żadnych zdarzeń|
|Magazyny/backupProtectableItems/odczytu|Zwraca listę wszystkich elementów podlegających ochronie|
|/vaults/replicationFabrics/Read|Żadnych sieci szkieletowych do odczytu|
|/vaults/replicationFabrics/Write|Utwórz lub zaktualizuj żadnych sieci szkieletowych|
|/vaults/replicationFabrics/Remove/Action|Usunięcie sieci szkieletowej|
|/vaults/replicationFabrics/checkConsistency/Action|Sprawdzanie spójności hello sieci szkieletowej|
|/vaults/replicationFabrics/DELETE|Usuń wszystkie sieci szkieletowe|
|/vaults/replicationFabrics/renewcertificate/Action||
|/vaults/replicationFabrics/deployProcessServerImage/Action|Wdróż obraz serwera przetwarzania|
|/vaults/replicationFabrics/reassociateGateway/Action|Ponownie Skojarz bramy|
|/ Magazyny/replicationFabrics/replicationRecoveryServicesProviders /<br>Odczyt|Przeczytaj wszystkich dostawców usług odzyskiwania|
|/ Magazyny/replicationFabrics/replicationRecoveryServicesProviders /<br>Usuń/działania|Usuń dostawcę usług odzyskiwania|
|/ Magazyny/replicationFabrics/replicationRecoveryServicesProviders /<br>Usuń|Usuwanie wszystkich dostawców usług odzyskiwania|
|/ Magazyny/replicationFabrics/replicationRecoveryServicesProviders /<br>refreshProvider/działania|Odśwież dostawcę|
|/vaults/replicationFabrics/replicationStorageClassifications/Read|Przeczytaj wszystkie klasyfikacje magazynu|
|/ Magazyny/replicationFabrics/replicationStorageClassifications /<br>replicationStorageClassificationMappings/Odczyt|Wszelkie mapowania klasyfikacji magazynu do odczytu|
|/ Magazyny/replicationFabrics/replicationStorageClassifications /<br>replicationStorageClassificationMappings/zapisu|Utwórz lub zaktualizuj wszystkie mapowania klasyfikacji magazynu|
|/ Magazyny/replicationFabrics/replicationStorageClassifications /<br>replicationStorageClassificationMappings/usuwania|Usuń wszelkie mapowania klasyfikacji magazynu|
|/vaults/replicationFabrics/replicationvCenters/Read|Wszystkie zadania do odczytu|
|/vaults/replicationFabrics/replicationvCenters/Write|Utwórz lub zaktualizuj wszystkie zadania|
|/vaults/replicationFabrics/replicationvCenters/DELETE|Usuń wszystkie zadania|
|/vaults/replicationFabrics/replicationNetworks/Read|Przeczytaj żadnych sieci|
|/ Magazyny/replicationFabrics/replicationNetworks /<br>replicationNetworkMappings/Odczyt|Przeczytaj wszelkie mapowania sieci|
|/ Magazyny/replicationFabrics/replicationNetworks /<br>replicationNetworkMappings/zapisu|Utwórz lub zaktualizuj wszystkie mapowania sieci|
|/ Magazyny/replicationFabrics/replicationNetworks /<br>replicationNetworkMappings/usuwania|Usuń wszelkie mapowania sieci|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>Odczyt|Wszystkie kontenery ochrony|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>discoverProtectableItem/działania|Odkryj element chronione|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>zapisu|Utwórz lub zaktualizuj kontenerach ochrony|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>Usuń/działania|Usunięcie kontenera ochrony|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>switchprotection/działania|Kontener ochrony przełącznika|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>replicationProtectableItems/Odczyt|Wszystkie chronione elementy do odczytu|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>replicationProtectionContainerMappings/Odczyt|Przeczytaj mapowań kontenera ochrony|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>replicationProtectionContainerMappings/zapisu|Utwórz lub zaktualizuj mapowań kontenera ochrony|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>replicationProtectionContainerMappings/usuwanie/działania|Usuń mapowanie kontenera ochrony|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>replicationProtectionContainerMappings/usuwania|Usuwanie mapowań kontenera ochrony|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>replicationProtectedItems/Odczyt|Wszystkie chronione elementy do odczytu|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>replicationProtectedItems/zapisu|Utwórz lub zaktualizuj wszystkie chronione elementy.|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>replicationProtectedItems/usuwania|Usuń wszystkie chronione elementy|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>replicationProtectedItems/usuwanie/działania|Usuwanie chronionego elementu|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>Akcja replicationProtectedItems/plannedFailover|Planowany tryb Failover|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>Akcja replicationProtectedItems/unplannedFailover|Tryb failover|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>Akcja replicationProtectedItems/testFailover|Testowanie trybu Failover|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>Akcja replicationProtectedItems/testFailoverCleanup|Wyczyszczenia testu pracy awaryjnej|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>Akcja replicationProtectedItems/failoverCommit|Zatwierdzanie trybu failover|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>Akcja replicationProtectedItems/ponownej ochrony|Włącz ponownie ochronę chronionego elementu|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>Akcja replicationProtectedItems/updateMobilityService|Aktualizacja usługi mobilności|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>Akcja replicationProtectedItems/repairReplication|Naprawa replikacji|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>Akcja replicationProtectedItems/applyRecoveryPoint|Zastosuj punktu odzyskiwania|
|/ Magazyny/replicationFabrics/replicationProtectionContainers /<br>replicationProtectedItems recoveryPoints/odczytu|Przeczytaj punktów odzyskiwania replikacji|
|/vaults/replicationPolicies/Read|Wszystkie zasady do odczytu|
|/vaults/replicationPolicies/Write|Utwórz lub zaktualizuj wszystkie zasady|
|/vaults/replicationPolicies/DELETE|Usuń wszystkie zasady|
|/vaults/replicationRecoveryPlans/Read|Wszystkie plany odzyskiwania do odczytu|
|/vaults/replicationRecoveryPlans/Write|Utwórz lub zaktualizuj wszystkie plany odzyskiwania|
|/vaults/replicationRecoveryPlans/DELETE|Usuń wszystkie plany odzyskiwania|
|/vaults/replicationRecoveryPlans/plannedFailover/Action|Plan odzyskiwania usługi planowanego trybu Failover|
|/vaults/replicationRecoveryPlans/unplannedFailover/Action|Plan odzyskiwania trybu failover|
|/vaults/replicationRecoveryPlans/testFailover/Action|Plan odzyskiwania trybu Failover testu|
|/vaults/replicationRecoveryPlans/testFailoverCleanup/Action|Plan odzyskiwania testu czyszczenia trybu Failover|
|/vaults/replicationRecoveryPlans/failoverCommit/Action|Zatwierdzanie trybu failover planu odzyskiwania|
|/vaults/replicationRecoveryPlans/reProtect/Action|Włącz ponownie ochronę planu odzyskiwania|
|Magazyny/extendedInformation/odczytu|Hello operacji Get Info rozszerzony pobiera obiekt rozszerzone informacje o reprezentujący hello zasobów platformy Azure typu? magazynu?|
|/ Magazyny/extendedInformation/zapisu|Hello operacji Get Info rozszerzony pobiera obiekt rozszerzone informacje o reprezentujący hello zasobów platformy Azure typu? magazynu?|
|/ Magazyny/extendedInformation/usuwania|Hello operacji Get Info rozszerzony pobiera obiekt rozszerzone informacje o reprezentujący hello zasobów platformy Azure typu? magazynu?|
|Magazyny/backupManagementMetaData/odczytu|Zwraca metadane zarządzania kopiami zapasowymi magazynu usług Recovery Services.|
|Magazyny/backupProtectionContainers/odczytu|Zwraca wszystkie kontenery należące toohello subskrypcji|
|Magazyny/backupFabrics/operationResults/odczytu|Zwraca stan operacji hello|
|Magazyny/backupFabrics/protectionContainers/odczytu|Zwraca wszystkich zarejestrowanych kontenerów|
|/ Magazyny/backupFabrics/protectionContainers /<br>operationResults/Odczyt|Pobiera wynik operacji wykonanej na kontenerze ochrony.|
|/ Magazyny/backupFabrics/protectionContainers /<br>protectedItems/Odczyt|Zwraca obiekt szczegóły hello chronionego elementu|
|/ Magazyny/backupFabrics/protectionContainers /<br>protectedItems/zapisu|Tworzenie kopii zapasowej elementu chronione|
|/ Magazyny/backupFabrics/protectionContainers /<br>protectedItems/usuwania|Usuwa chronionego elementu|
|/ Magazyny/backupFabrics/protectionContainers /<br>Akcja protectedItems/tworzenia kopii zapasowej|Wykonuje kopię zapasową elementu chronionego.|
|/ Magazyny/backupFabrics/protectionContainers /<br>protectedItems operationResults/odczytu|Pobiera wynik operacji wykonanej na elementach chronionych.|
|/ Magazyny/backupFabrics/protectionContainers /<br>protectedItems operationStatus/odczytu|Zwraca stan hello operację na chronione elementy.|
|/ Magazyny/backupFabrics/protectionContainers /<br>protectedItems recoveryPoints/odczytu|Pobierz punkty odzyskiwania dla elementów chronionych.|
|/ Magazyny/backupFabrics/protectionContainers /<br>protectedItems/recoveryPoints /<br>Akcja/przywracania|Przywróć punkty odzyskiwania dla elementów chronionych.|
|/ Magazyny/backupFabrics/protectionContainers /<br>protectedItems/recoveryPoints /<br>provisionInstantItemRecovery/działania|Odzyskiwanie elementów błyskawicznych udostępniania dla chronionego elementu|
|/ Magazyny/backupFabrics/protectionContainers /<br>protectedItems/recoveryPoints /<br>revokeInstantItemRecovery/działania|Odwołanie elementu błyskawicznych odzyskiwania dla chronionego elementu|
|Magazyny/użycia/odczytu|Zwraca szczegóły użycia magazynu usług Recovery Services.|
|/vaults/Usages/Read|Przeczytaj również użycia magazynu|
|/ Magazyny/certyfikatów/zapisu|Hello operacja aktualizacji zasobów certyfikatu aktualizuje certyfikat poświadczeń hello zasobów/magazynu.|
|Magazyny/tokenInfo/odczytu|Zwraca token informacje magazynie usług odzyskiwania.|
|/vaults/replicationAlertSettings/Read|Wszystkie ustawienia alertów do odczytu|
|/vaults/replicationAlertSettings/Write|Utwórz lub zaktualizuj ustawienia alertów|
|Magazyny/backupOperations/odczytu|Zwraca operacji tworzenia kopii zapasowej odzyskiwania stanu usługi magazynu.|
|Magazyny/storageConfig/odczytu|Zwraca konfigurację magazynu dla odzyskiwania usług magazynu.|
|/ Magazyny/storageConfig/zapisu|Aktualizacje konfiguracji magazynu dla odzyskiwania usług magazynu.|
|Magazyny/backupUsageSummaries/odczytu|Zwraca podsumowania dla chronionych serwerów i chronione elementy usług odzyskiwania.|
|Magazyny/backupProtectedItems/odczytu|Zwraca listę hello wszystkie chronione elementy.|
|Magazyny/backupconfig/vaultconfig/odczytu|Zwraca konfigurację Recovery usług magazynu.|
|/ Magazyny/backupconfig/vaultconfig/zapisu|Konfigurowanie aktualizacji odzyskiwania usług magazynu.|
|/ Magazyny/registeredIdentities/zapisu|Hello operacji zarejestrować kontenera usług mogą być używane tooregister kontener z usługą odzyskiwania.|
|Magazyny/registeredIdentities/odczytu|Pobrać kontenery Hello, można użyć operacji Pobierz hello kontenery zarejestrowanych dla zasobu.|
|/ Magazyny/registeredIdentities/usuwania|Hello wyrejestrować kontenera operacji może być używane toounregister kontenera.|
|Magazyny/registeredIdentities/operationResults/odczytu|Operacja przesłane Hello wyniki operacji Get można stan operacji get używane hello i spowodują przez hello asynchronicznie operację|
|/vaults/replicationJobs/Read|Wszystkie zadania do odczytu|
|/vaults/replicationJobs/Cancel/Action|Anulowanie zadania|
|/vaults/replicationJobs/restart/Action|Uruchom ponownie zadanie|
|/vaults/replicationJobs/resume/Action|Wznów zadanie|
|Magazyny/backupPolicies/odczytu|Zwraca wszystkie zasady ochrony|
|/ Magazyny/backupPolicies/zapisu|Tworzy zasady ochrony|
|/ Magazyny/backupPolicies/usuwania|Usuń zasady ochrony|
|Magazyny/backupPolicies/operationResults/odczytu|Pobierz wyniki operacji zasad.|
|Magazyny/backupPolicies/operationStatus/odczytu|Pobierz stan operacji zasad.|
|Magazyny/vaultTokens/odczytu|Hello magazynu Token operacji może być używane tooget magazynu tokenu dla operacji poziomu wewnętrznej bazy danych magazynu.|
|Magazyny/monitoringConfigurations/notificationConfiguration/odczytu|Pobiera konfigurację powiadomień magazynu usług odzyskiwania hello.|
|Magazyny/backupJobs/odczytu|Zwraca wszystkie obiekty zadania|
|/ Magazyny/backupJobs / / akcję anulowania|Anuluj hello zadania|
|Magazyny/backupJobs/operationResults/odczytu|Zwraca hello operacja wyniku zadania.|
|/Locations/allocateStamp/Action|AllocateStamp jest używane przez usługę operacji wewnętrznych|
|/Locations/allocatedStamp/Read|Operacja GetAllocatedStamp to operacja wewnętrzna używana przez usługę|

## <a name="microsoftrelay"></a>Microsoft.Relay

| Operacja | Opis |
|---|---|
|/ checkNamespaceAvailability/działania|Sprawdza dostępność przestrzeni nazw w ramach danej subskrypcji.|
|/ register/działania|Rejestruje hello subskrypcji dla dostawcy zasobów przekazywania hello i umożliwia tworzenie hello przekazywania zasobów|
|/ przestrzenie nazw/zapisu|Utwórz zasób Namespace i zaktualizuj jego właściwości. Znaczniki i stan hello Namespace są hello właściwości, które mogą być aktualizowane.|
|/Namespaces/Read|Pobierz listę hello Namespace opis zasobu|
|przestrzenie nazw/Delete|Usuń zasób Namespace|
|/Namespaces/authorizationRules/Write|Tworzenie reguł autoryzacji z poziomu Namespace i aktualizowanie jej właściwości. Prawa dostępu reguł autoryzacji Hello, hello podstawowej i dodatkowej klucze mogą być aktualizowane.|
|/Namespaces/authorizationRules/DELETE|Usuń regułę autoryzacji Namespace. Nie można usunąć Hello domyślna reguła autoryzacji Namespace. |
|/Namespaces/authorizationRules/listkeys/Action|Pobierz toohello parametry połączenia hello Namespace|
|/Namespaces/HybridConnections/Write|Tworzenie lub aktualizacja HybridConnection właściwości.|
|/Namespaces/HybridConnections/Read|Pobierz listę opisów zasobów HybridConnection|
|/Namespaces/HybridConnections/DELETE|Operacja toodelete HybridConnection zasobów|
|/Namespaces/HybridConnections/authorizationRules/Write|Tworzenie reguł autoryzacji HybridConnection i aktualizowanie jej właściwości. Prawa dostępu reguł autoryzacji Hello, hello podstawowej i dodatkowej klucze mogą być aktualizowane.|
|/Namespaces/HybridConnections/authorizationRules/DELETE|Operacja toodelete HybridConnection reguł autoryzacji|
|/Namespaces/HybridConnections/authorizationRules/listkeys/Action|Pobierz hello tooHybridConnection parametry połączenia|
|/Namespaces/WcfRelays/Write|Tworzenie lub aktualizacja WcfRelay właściwości.|
|/Namespaces/WcfRelays/Read|Pobierz listę opisów zasobów WcfRelay|
|/Namespaces/WcfRelays/DELETE|Operacja toodelete WcfRelay zasobów|
|/Namespaces/WcfRelays/authorizationRules/Write|Tworzenie reguł autoryzacji WcfRelay i aktualizowanie jej właściwości. Prawa dostępu reguł autoryzacji Hello, hello podstawowej i dodatkowej klucze mogą być aktualizowane.|
|/Namespaces/WcfRelays/authorizationRules/DELETE|Operacja toodelete WcfRelay reguł autoryzacji|
|/Namespaces/WcfRelays/authorizationRules/listkeys/Action|Pobierz hello tooWcfRelay parametry połączenia|

## <a name="microsoftresourcehealth"></a>Microsoft.ResourceHealth

| Operacja | Opis |
|---|---|
|AvailabilityStatuses/odczytu|Pobiera stany dostępności hello wszystkich zasobów w hello określony zakres|
|AvailabilityStatuses/bieżącego/odczytu|Pobiera stan dostępności hello hello określony zasób|

## <a name="microsoftresources"></a>Microsoft.Resources

| Operacja | Opis |
|---|---|
|/ checkResourceName/działania|Sprawdź poprawność nazwy zasobu hello.|
|/Providers/Read|Pobierz hello listę dostawców.|
|/Subscriptions/Read|Pobiera listę hello subskrypcji.|
|/Subscriptions/operationresults/Read|Uzyskanie subskrypcji hello wyniki operacji.|
|/Subscriptions/Providers/Read|Pobiera dostawców zasobów lub wyświetla ich listę.|
|/Subscriptions/tagNames/Read|Pobiera tagi subskrypcji lub wyświetla ich listę.|
|/Subscriptions/tagNames/Write|Dodaje tag subskrypcji.|
|/Subscriptions/tagNames/DELETE|Usuwa tag subskrypcji.|
|/Subscriptions/tagNames/tagValues/Read|Pobiera wartości tagów lub wyświetla ich listę.|
|/Subscriptions/tagNames/tagValues/Write|Dodaje wartość tagu subskrypcji.|
|/Subscriptions/tagNames/tagValues/DELETE|Usuwa wartość tagu subskrypcji.|
|/Subscriptions/Resources/Read|Pobiera zasoby subskrypcji.|
|/Subscriptions/resourceGroups/Read|Pobiera grupy zasobów lub wyświetla ich listę.|
|/Subscriptions/resourceGroups/Write|Tworzy lub aktualizuje grupę zasobów.|
|/Subscriptions/resourceGroups/DELETE|Usuwa grupę zasobów i wszystkie zasoby w tej grupie.|
|/Subscriptions/resourceGroups/moveResources/Action|Przenosi zasoby z tooanother grupy jeden zasób.|
|/Subscriptions/resourceGroups/validateMoveResources/Action|Waliduj przeniesienie zasobów z jednego zasobu tooanother grupy.|
|/Subscriptions/resourcegroups/Resources/Read|Pobiera zasoby hello hello grupy zasobów.|
|/Subscriptions/resourcegroups/Deployments/Read|Pobiera wdrożenia lub wyświetla ich listę.|
|/Subscriptions/resourcegroups/Deployments/Write|Tworzy lub aktualizuje wdrożenie.|
|/Subscriptions/resourcegroups/Deployments/operationstatuses/Read|Pobiera lub wyświetla stany operacji wdrażania.|
|/Subscriptions/resourcegroups/Deployments/Operations/Read|Pobiera operacje wdrażania lub wyświetla ich listę.|
|/Subscriptions/Locations/Read|Pobiera hello listę obsługiwanych lokalizacji.|
|/Links/Read|Pobiera linki do zasobów lub wyświetla ich listę.|
|/ łącza/zapisu|Tworzy lub aktualizuje link do zasobu.|
|/Links/DELETE|Usuwa link do zasobu.|
|/tenants/Read|Pobiera listę hello dzierżawców.|
|/Resources/Read|Pobierz hello listę zasobów zgodnie z filtrami.|
|/Deployments/Read|Pobiera wdrożenia lub wyświetla ich listę.|
|/ wdrożeń/zapisu|Tworzy lub aktualizuje wdrożenie.|
|/Deployments/DELETE|Usuwa wdrożenie.|
|/Deployments/Cancel/Action|Anuluje wdrożenie.|
|/Deployments/Validate/Action|Weryfikuje wdrożenie.|
|/Deployments/Operations/Read|Pobiera operacje wdrażania lub wyświetla ich listę.|

## <a name="microsoftscheduler"></a>Microsoft.Scheduler

| Operacja | Opis |
|---|---|
|/jobcollections/Read|Pobierz kolekcję zadań|
|/ kolekcjach zadań/zapisu|Tworzy lub aktualizuje kolekcję zadań.|
|/jobcollections/DELETE|Usuwa zadania kolekcji.|
|/jobcollections/enable/Action|Włącza zadanie kolekcji.|
|/jobcollections/disable/Action|Wyłącza zadanie kolekcji.|
|/jobcollections/Jobs/Read|Pobiera zadanie.|
|/jobcollections/Jobs/Write|Tworzy lub aktualizuje zadanie.|
|/jobcollections/Jobs/DELETE|Usuwa zadanie.|
|/jobcollections/Jobs/Run/Action|Uruchamia zadanie.|
|/jobcollections/Jobs/generateLogicAppDefinition/Action|Generuje definicję aplikacji logiki na podstawie zadania usługi Scheduler.|
|/jobcollections/Jobs/jobhistories/Read|Pobiera Historia zadania.|

## <a name="microsoftsearch"></a>Microsoft.Search

| Operacja | Opis |
|---|---|
|/ register/działania|Rejestruje hello subskrypcji dla dostawcy zasobów hello wyszukiwania i umożliwia tworzenie hello usługi wyszukiwania.|
|/ checkNameAvailability/działania|Sprawdza dostępność hello nazwy usługi.|
|/ searchServices/zapisu|Tworzy lub aktualizuje hello usługi wyszukiwania.|
|/searchServices/Read|Odczytuje hello usługi wyszukiwania.|
|/searchServices/DELETE|Usuwa hello usługi wyszukiwania.|
|/searchServices/Start/Action|Uruchamia usługę wyszukiwania hello.|
|/searchServices/Stop/Action|Zatrzymuje usługę wyszukiwania hello.|
|/searchServices/listAdminKeys/Action|Odczytuje hello kluczy administratora.|
|/searchServices/regenerateAdminKey/Action|Generuje ponownie hello klucz administratora.|
|/searchServices/createQueryKey/Action|Tworzy hello klucza zapytania.|
|/searchServices/queryKey/Read|Odczytuje hello klucze zapytania.|
|/searchServices/queryKey/DELETE|Usuwa hello klucza zapytania.|

## <a name="microsoftsecurity"></a>Microsoft.Security

| Operacja | Opis |
|---|---|
|/jitNetworkAccessPolicies/Read|Pobiera zasady dostępu do sieci w czasie hello|
|/ jitNetworkAccessPolicies/zapisu|Tworzy nowe zasady dostępu do sieci w czasie, lub aktualizuje istniejący zestaw|
|/jitNetworkAccessPolicies/initiate/Action|Inicjuje zasady dostępu do sieci w czasie|
|/securitySolutionsReferenceData/Read|Pobiera dane referencyjne hello rozwiązań zabezpieczeń|
|/securityStatuses/Read|Pobiera stany kondycji hello zabezpieczeń zasobów platformy Azure|
|/webApplicationFirewalls/Read|Pobiera zapór aplikacji sieci web hello|
|/ webApplicationFirewalls/zapisu|Nowa Zapora aplikacji sieci web tworzy lub aktualizuje istniejący zestaw|
|/webApplicationFirewalls/DELETE|Usuwa zapory aplikacji sieci web|
|/securitySolutions/Read|Pobiera hello rozwiązań zabezpieczeń|
|/ securitySolutions/zapisu|Tworzy nowe rozwiązanie zabezpieczeń lub aktualizuje istniejący zestaw|
|/securitySolutions/DELETE|Usuwa rozwiązania zabezpieczeń|
|/Tasks/Read|Pobiera wszystkie zalecenia dotyczące zabezpieczeń dostępne|
|/Tasks/dismiss/Action|Odrzuć zalecana ze względów bezpieczeństwa|
|/Tasks/Activate/Action|Aktywuj zalecana ze względów bezpieczeństwa|
|/Policies/Read|Pobiera hello zasady zabezpieczeń|
|/ zasady/zapisu|Aktualizacje hello zasady zabezpieczeń|
|/applicationWhitelistings/Read|Pobiera whitelistings aplikacji hello|
|/ applicationWhitelistings/zapisu|Tworzy nowy listę dozwolonych aplikacji podobnej lub aktualizuje istniejący zestaw|

## <a name="microsoftservermanagement"></a>Microsoft.ServerManagement

| Operacja | Opis |
|---|---|
|/ subscriptions/zapisu|Tworzy lub aktualizuje subskrypcji|
|/ bram/zapisu|Tworzy lub aktualizuje bramy|
|/Gateways/DELETE|Usuwa bramę|
|/Gateways/Read|Pobiera bramy|
|/Gateways/regenerateprofile/Action|Generuje ponownie hello bramy profilu|
|/Gateways/upgradetolatest/Action|Uaktualnienia hello bramy toohello najnowszej wersji|
|/ węzły/zapisu|Tworzy lub aktualizuje węzła|
|/nodes/DELETE|Usuwa węzła|
|/nodes/Read|Pobiera węzeł|
|/ sesje/zapisu|Tworzy lub aktualizuje sesji|
|/Sessions/Read|Pobiera sesję|
|/Sessions/DELETE|Usuwa sesssion|

## <a name="microsoftservicebus"></a>Microsoft.ServiceBus

| Operacja | Opis |
|---|---|
|/ checkNameAvailability/działania|Sprawdza dostępność przestrzeni nazw w ramach danej subskrypcji.|
|/ register/działania|Rejestruje hello subskrypcji dla dostawcy zasobów hello magistrali usług i umożliwia tworzenie hello zasobów magistrali usług|
|/ przestrzenie nazw/zapisu|Utwórz zasób Namespace i zaktualizuj jego właściwości. Znaczniki i stan hello Namespace są hello właściwości, które mogą być aktualizowane.|
|/Namespaces/Read|Pobierz listę hello Namespace opis zasobu|
|przestrzenie nazw/Delete|Usuń zasób Namespace|
|/Namespaces/metricDefinitions/Read|Pobierz listę metryki Namespace opisów zasobów|
|/Namespaces/authorizationRules/Write|Tworzenie reguł autoryzacji z poziomu Namespace i aktualizowanie jej właściwości. Prawa dostępu reguł autoryzacji Hello, hello podstawowej i dodatkowej klucze mogą być aktualizowane.|
|/Namespaces/authorizationRules/Read|Pobierz listę hello opis reguły autoryzacji przestrzeni nazw.|
|/Namespaces/authorizationRules/DELETE|Usuń regułę autoryzacji Namespace. Nie można usunąć Hello domyślna reguła autoryzacji Namespace. |
|/Namespaces/authorizationRules/listkeys/Action|Pobierz toohello parametry połączenia hello Namespace|
|/Namespaces/authorizationRules/regenerateKeys/Action|Wygeneruj ponownie hello podstawowej lub pomocniczej klucza toohello zasobów|
|/Namespaces/diagnosticSettings/Read|Pobierz listę Namespace ustawień diagnostycznych zasobu opisów|
|/Namespaces/diagnosticSettings/Write|Pobierz listę Namespace ustawień diagnostycznych zasobu opisów|
|/Namespaces/Queues/Write|Utwórz lub właściwości kolejki aktualizacji.|
|/Namespaces/Queues/Read|Pobierz listę opisów zasobów kolejki|
|/Namespaces/Queues/DELETE|Operacja toodelete kolejki zasobów|
|/Namespaces/Queues/authorizationRules/Write|Tworzenie reguł autoryzacji kolejki i aktualizowanie jej właściwości. Prawa dostępu reguł autoryzacji Hello, hello podstawowej i dodatkowej klucze mogą być aktualizowane.|
|/Namespaces/Queues/authorizationRules/Read| Pobierz listę hello kolejki reguł autoryzacji|
|/Namespaces/Queues/authorizationRules/DELETE|Operacja toodelete kolejki reguł autoryzacji|
|/Namespaces/Queues/authorizationRules/listkeys/Action|Pobierz hello tooQueue parametry połączenia|
|/Namespaces/Queues/authorizationRules/regenerateKeys/Action|Wygeneruj ponownie hello podstawowej lub pomocniczej klucza toohello zasobów|
|/Namespaces/logDefinitions/Read|Pobierz listę dzienników Namespace opisów zasobów|
|/Namespaces/topics/Write|Tworzenie lub aktualizacja tematu właściwości.|
|/Namespaces/topics/Read|Pobierz listę opisów zasobów tematu|
|/Namespaces/topics/DELETE|Operacja toodelete zasobów tematu|
|/Namespaces/topics/authorizationRules/Write|Tworzenie reguł autoryzacji tematu i aktualizowanie jej właściwości. Prawa dostępu reguł autoryzacji Hello, hello podstawowej i dodatkowej klucze mogą być aktualizowane.|
|/Namespaces/topics/authorizationRules/Read| Pobierz listę hello temat reguł autoryzacji|
|/Namespaces/topics/authorizationRules/DELETE|Operacja toodelete temat reguł autoryzacji|
|/Namespaces/topics/authorizationRules/listkeys/Action|Pobierz hello tooTopic parametry połączenia|
|/Namespaces/topics/authorizationRules/regenerateKeys/Action|Wygeneruj ponownie hello podstawowej lub pomocniczej klucza toohello zasobów|
|/Namespaces/topics/Subscriptions/Write|Tworzenie lub aktualizacja TopicSubscription właściwości.|
|/Namespaces/topics/Subscriptions/Read|Pobierz listę opisów zasobów TopicSubscription|
|/Namespaces/topics/Subscriptions/DELETE|Operacja toodelete TopicSubscription zasobów|
|/Namespaces/topics/Subscriptions/Rules/Write|Tworzenie lub aktualizacja reguły właściwości.|
|/Namespaces/topics/Subscriptions/Rules/Read|Pobierz listę reguł opisów zasobów|
|/Namespaces/topics/Subscriptions/Rules/DELETE|Operacja toodelete zasobu reguły|

## <a name="microsoftsql"></a>Microsoft.Sql

| Operacja | Opis |
|---|---|
|/Servers/Read|Zwraca listę serwerów w grupie zasobów w subskrypcji|
|/ serwery/zapisu|Utwórz nowy serwer lub zmodyfikować właściwości istniejącego serwera w grupie zasobów w subskrypcji|
|/Servers/DELETE|Usuń serwer i wszystkie zawarte bazy danych i pul elastycznych|
|/Servers/Import/Action|Utwórz nową bazę danych na serwerze hello i wdrażanie schemat i dane z pakietu DacPac|
|/Servers/Upgrade/Action|Włącz nowe funkcje dostępne w najnowszej wersji serwera hello i określ mapy konwersji wersji bazy danych|
|/Servers/VulnerabilityAssessmentScans/Action|Wykonywanie skanowania serwera w celu oceny luk w zabezpieczeniach|
|/Servers/operationResults/Read|Operacja jest używana tootrack postęp uaktualniania serwera z niższym toohigher wersji|
|/Servers/operationResults/DELETE|Przerwanie uaktualniania wersji serwera w toku|
|/Servers/securityAlertPolicies/Read|Pobieranie szczegółów powitania serwera zagrożeń wykrywania zasady skonfigurowane na danym serwerze|
|/Servers/securityAlertPolicies/Write|Zmień hello wykrywanie zagrożeń serwera dla danego serwera|
|/Servers/securityAlertPolicies/operationResults/Read|Pobierz wyniki powitania serwera zasady wykrywania zagrożeń operacji Set|
|/Servers/Administrators/Read|Pobieranie szczegółów administratora serwera|
|/Servers/Administrators/Write|Utwórz lub zaktualizuj administratora serwera|
|/Servers/Administrators/DELETE|Usunąć administratora z powitania serwera|
|/Servers/recoverableDatabases/Read|Ta operacja jest używana do odzyskiwania po awarii na żywo bazy danych toorestore bazy danych toolast znaną dobrą punktu kopii zapasowej. Zwraca informacje o ostatnim dobrej kopii zapasowej hello, ale faktycznie nie go przywrócić hello bazy danych.|
|/Servers/serviceObjectives/Read|Pobieranie listy celów poziomu usługi (znanej także jako warstwy wydajności) dostępnych na danym serwerze|
|/Servers/firewallRules/Read|Pobieranie szczegółów reguły zapory serwera|
|/Servers/firewallRules/Write|Utwórz lub zaktualizuj reguły zapory serwera, która określa zakres adresów IP dozwolone tooconnect toohello serwera|
|/Servers/firewallRules/DELETE|Usuń regułę zapory z powitania serwera|
|/Servers/administratorOperationResults/Read|Pobiera wyniki operacji administratora serwera|
|/Servers/recommendedElasticPools/Read|Pobierz zalecenia dotyczące koszt tooreduce puli elastycznej bazy danych lub zwiększenia wydajności na podstawie wykorzystania zasobów historica|
|/Servers/recommendedElasticPools/Metrics/Read|Pobrać metryki dla zalecane elastyczne pule baz danych dla danego serwera|
|/Servers/recommendedElasticPools/Databases/Read|Pobrać baz danych, które mają zostać dodane do zalecane elastyczne pule baz danych dla danego serwera|
|/Servers/elasticPools/Read|Pobieranie szczegółów elastycznej puli baz danych na danym serwerze|
|/Servers/elasticPools/Write|Utwórz nową lub zmodyfikować właściwości istniejącej puli elastycznej bazy danych|
|/Servers/elasticPools/DELETE|Usuń istniejącej puli elastycznej bazy danych|
|/Servers/elasticPools/operationResults/Read|Pobieranie szczegółów w operacji puli elastycznej bazy danych|
|/Servers/elasticPools/Providers/Microsoft.Insights/<br>metricDefinitions/Odczyt|Zwracane typy metryk, które są dostępne dla elastycznych pul baz danych|
|/Servers/elasticPools/Providers/Microsoft.Insights/<br>diagnosticSettings/Odczyt|Pobiera hello ustawienie diagnostyczne dla zasobu hello|
|/Servers/elasticPools/Providers/Microsoft.Insights/<br>diagnosticSettings/zapisu|Tworzy lub aktualizuje hello ustawienie diagnostyczne dla zasobu hello|
|/Servers/elasticPools/Metrics/Read|Zwraca metryki użycia zasobów puli elastycznej bazy danych|
|/Servers/elasticPools/elasticPoolDatabaseActivity/Read|Pobieranie działań i szczegóły dotyczące danego bazy danych, która jest częścią puli elastycznej bazy danych|
|/Servers/elasticPools/advisors/Read|Zwraca listę dostępnych dla puli elastycznej hello doradcy|
|/Servers/elasticPools/advisors/Write|Aktualizacja automatycznego wykonywania stanu usługi advisor na poziomie puli elastycznej.|
|/Servers/elasticPools/advisors/recommendedActions/Read|Zwraca listę zalecane działania advisor określony dla puli elastycznej hello|
|/Servers/elasticPools/advisors/recommendedActions/Write|Zastosuj hello Zalecana akcja na powitania puli elastycznej|
|/Servers/elasticPools/elasticPoolActivity/Read|Pobieranie działań i szczegółowe informacje o puli elastycznej bazy danych|
|/Servers/elasticPools/Databases/Read|Pobieranie listy i szczegółów baz danych, które są częścią puli elastycznej bazy danych na danym serwerze|
|/Servers/auditingPolicies/Read|Pobieranie szczegółów tabeli serwera domyślnego hello skonfigurowane na danym serwerze zasady inspekcji|
|/Servers/auditingPolicies/Write|Zmiana tabeli serwera domyślnego hello inspekcji dla danego serwera|
|/Servers/disasterRecoveryConfiguration/operationResults/Read|Pobierz wyniki operacji konfiguracji odzyskiwania po awarii|
|/Servers/advisors/Read|Zwraca listę doradcy jest dostępna dla powitania serwera|
|/Servers/advisors/Write|Aktualizacje automatyczne execute stanu usługi advisor na poziomie serwera.|
|/Servers/advisors/recommendedActions/Read|Zwraca listę zalecane działania określonej usługi advisor na powitania serwera|
|/Servers/advisors/recommendedActions/Write|Zastosuj hello Zalecana akcja na powitania serwera|
|/Servers/Usages/Read|Zwraca limit przydziału jednostek dtu w warstwie serwera i bieżący consuption jednostek dtu w warstwie przez wszystkie bazy danych w ramach powitania serwera|
|/Servers/elasticPoolEstimates/Read|Zwraca listę już utworzone dla tego serwera oszacowania puli elastycznej|
|/Servers/elasticPoolEstimates/Write|Tworzy nowego szacowania puli elastycznej dla listy baz danych, pod warunkiem|
|/Servers/auditingSettings/Read|Pobieranie szczegółów obiektu blob serwera hello skonfigurowane na danym serwerze zasady inspekcji|
|/Servers/auditingSettings/Write|Zmień powitania serwera obiektu blob inspekcji dla danego serwera|
|/Servers/auditingSettings/operationResults/Read|Pobierz wynik powitania serwera blob inspekcji operacji zestawu zasad|
|/Servers/backupLongTermRetentionVaults/Read|Ta operacja jest używana tooget magazyn przechowywania długoterminowej kopii zapasowej. Zwraca informacje dotyczące hello magazynu toothis zarejestrowanego serwera.|
|/Servers/backupLongTermRetentionVaults/Write|Zarejestruj w magazynie przechowywania długoterminowej kopii zapasowej|
|/Servers/restorableDroppedDatabases/Read|Pobieranie listy baz danych, które zostały usunięte na danym serwerze znajdujące się nadal w ramach zasad przechowywania. Ta operacja zwraca listę baz danych i skojarzonymi metadanymi, takich jak Data usunięcia.|
|/Servers/Databases/Read|Zwraca listę serwerów w grupie zasobów w subskrypcji|
|/Servers/Databases/Write|Utwórz nowy serwer lub zmodyfikować właściwości istniejącego serwera w grupie zasobów w subskrypcji|
|/Servers/Databases/DELETE|Usuń serwer i wszystkie zawarte bazy danych i pul elastycznych|
|/Servers/Databases/Export/Action|Utwórz nową bazę danych na serwerze hello i wdrażanie schemat i dane z pakietu DacPac|
|/Servers/Databases/VulnerabilityAssessmentScans/Action|Wykonywanie skanowania bazy danych w celu oceny luk w zabezpieczeniach.|
|/Servers/Databases/pause/Action|Wstrzymaj wersji bazy danych magazynu danych|
|/Servers/Databases/resume/Action|Wznów wersji bazy danych magazynu danych|
|/Servers/Databases/operationResults/Read|Operacja jest używana tootrack postępu długotrwałej operacji bazy danych, takich jak skali.|
|/Servers/Databases/replicationLinks/Read|Zwracany szczegółów dotyczących łącz replikacji dla określonej bazy danych|
|/Servers/Databases/replicationLinks/DELETE|Zakończenie relacji replikacji hello wymuszone i o utracie danych|
|/Servers/Databases/replicationLinks/unlink/Action|Zakończenie relacji replikacji hello wymuszone lub po synchronizacji z partnerem hello|
|/Servers/Databases/replicationLinks/Failover/Action|Trybu failover po synchronizacji wszystkie zmiany z hello podstawowego, co ta baza danych w relacji replikacji hello hello głównych i wprowadzania zdalnego podstawowej do dodatkowej|
|/Servers/Databases/replicationLinks/forceFailoverAllowDataLoss/Action|Tryb failover natychmiast o utracie danych, co ta baza danych w relacji replikacji hello hello głównych i wprowadzania zdalnego podstawowej do dodatkowej|
|/Servers/Databases/replicationLinks/updateReplicationMode/Action|Aktualizacja trybu replikacji dla łącza toosynchronous lub asynchroniczne|
|/Servers/Databases/replicationLinks/operationResults/Read|Pobierz stan operacji długotrwałych w łączach replikacji bazy danych|
|/Servers/Databases/dataMaskingPolicies/Read|Pobieranie szczegółów danych hello maskowania zasady skonfigurowane na danym bazy danych|
|/Servers/Databases/dataMaskingPolicies/Write|Zmień zasady dla danych maskowania danych|
|/Servers/Databases/dataMaskingPolicies/Rules/Read|Pobieranie szczegółów danych hello maskowania regułę skonfigurowany w danej bazie danych|
|/Servers/Databases/dataMaskingPolicies/Rules/Write|Zmień dane maskowania reguły określonej bazy danych|
|/Servers/Databases/securityAlertPolicies/Read|Pobieranie szczegółów zasady wykrywania zagrożeń hello skonfigurowany w danej bazie danych|
|/Servers/Databases/securityAlertPolicies/Write|Zmień zasady wykrywania zagrożeń hello określonej bazy danych|
|/Servers/Databases/Providers/Microsoft.Insights/<br>metricDefinitions/Odczyt|Zwracane typy metryk, które są dostępne dla baz danych|
|/Servers/Databases/Providers/Microsoft.Insights/<br>diagnosticSettings/Odczyt|Pobiera hello ustawienie diagnostyczne dla zasobu hello|
|/Servers/Databases/Providers/Microsoft.Insights/<br>diagnosticSettings/zapisu|Tworzy lub aktualizuje hello ustawienie diagnostyczne dla zasobu hello|
|/Servers/Databases/Providers/Microsoft.Insights/<br>logDefinitions/Odczyt|Pobiera dostępne dzienniki hello baz danych|
|/Servers/Databases/topQueries/Read|Zwraca zagregowane statystyk czasu wykonywania dla wybranego zapytania w wybranym okresie|
|/Servers/Databases/topQueries/queryText/Read|Zwraca tekst języka Transact-SQL hello wybrane zapytanie o identyfikatorze|
|/Servers/Databases/topQueries/statistics/Read|Zwraca zagregowane statystyk czasu wykonywania dla wybranego zapytania w wybranym okresie|
|/Servers/Databases/connectionPolicies/Read|Pobieranie szczegółów hello połączenia zasady skonfigurowane na danym bazy danych|
|/Servers/Databases/connectionPolicies/Write|Zmień zasady połączenia dla danego bazy danych|
|/Servers/Databases/Metrics/Read|Zwraca metryki użycia zasobów bazy danych|
|/Servers/Databases/auditRecords/Read|Pobieranie rekordów inspekcji obiektu blob, hello bazy danych|
|/Servers/Databases/transparentDataEncryption/Read|Pobieranie stanu i szczegółowe informacje o funkcji zabezpieczeń szyfrowania danych przezroczysty określonej bazy danych|
|/Servers/Databases/transparentDataEncryption/Write|Włącz lub wyłącz przezroczystego szyfrowania danych określonej bazy danych|
|/Servers/Databases/transparentDataEncryption/operationResults/Read|Pobieranie stanu i szczegółowe informacje o funkcji zabezpieczeń szyfrowania danych przezroczysty określonej bazy danych|
|/Servers/Databases/auditingPolicies/Read|Pobieranie szczegółów zasady inspekcji tabeli hello skonfigurowany w danej bazie danych|
|/Servers/Databases/auditingPolicies/Write|Zmień zasady inspekcji tabeli hello określonej bazy danych|
|/Servers/Databases/dataWarehouseQueries/Read|Zwraca hello informacji zapytania dystrybucji magazynu danych dla Identyfikatora wybranego zapytania|
|/ serwery baz danych/dataWarehouseQueries /<br>dataWarehouseQuerySteps/Odczyt|Zwraca hello rozproszone zapytania informacje krok zapytania magazynu danych dla Identyfikatora wybrany krok|
|/Servers/Databases/serviceTierAdvisors/Read|Zwraca sugestii dotyczących skalowania bazy danych w górę lub w dół na podstawie wydajności tooimprove statystyk wykonywania zapytań lub zmniejszyć koszt|
|/Servers/Databases/advisors/Read|Zwraca listę dostępnych dla bazy danych hello doradcy|
|/Servers/Databases/advisors/Write|Aktualizacja automatycznego wykonywania stanu usługi advisor na poziomie bazy danych.|
|/Servers/Databases/advisors/recommendedActions/Read|Zwraca listę zalecanych akcji określonej advisor hello bazy danych|
|/Servers/Databases/advisors/recommendedActions/Write|Zastosuj hello Zalecana akcja na powitania bazy danych|
|/Servers/Databases/Usages/Read|Zwraca rozmiar maksymalny bazy danych, która może być osiągnięta i bieżący rozmiar zajmowane przez|
|/Servers/Databases/queryStore/Read|Zwraca bieżące wartości ustawień magazyn zapytań dla bazy danych hello|
|/Servers/Databases/queryStore/Write|Aktualizuje ustawienia magazynu zapytań dla bazy danych hello|
|/Servers/Databases/auditingSettings/Read|Pobieranie szczegółów zasady inspekcji obiektu blob hello skonfigurowany w danej bazie danych|
|/Servers/Databases/auditingSettings/Write|Zmień zasady inspekcji obiektu blob hello określonej bazy danych|
|/Servers/Databases/schemas/Tables/recommendedIndexes/Read|Pobieranie listy zalecenia dotyczące indeksu dla bazy danych|
|/Servers/Databases/schemas/Tables/recommendedIndexes/Write|Zastosuj zalecenie dotyczące indeksu|
|/Servers/Databases/schemas/Tables/Columns/Read|Pobieranie listy kolumn tabeli.|
|/Servers/Databases/missingindexes/Read|Zwraca sugestie dotyczące toocreate indeksy bazy danych, modyfikować lub usuwać w kolejności tooimprove kwerendy wydajności|
|/Servers/Databases/missingindexes/Write|Użyj bazy danych zalecenie dotyczące indeksu w określonej bazy danych|
|/Servers/Databases/importExportOperationResults/Read|Zwraca szczegółowe informacje o importu bazy danych lub operacji eksportowania z DacPac znajdujących się na koncie magazynu|
|/Servers/importExportOperationResults/Read|Zwraca listę hello w szczegółowych informacjach dotyczących operacji importu bazy danych z konta magazynu na danym serwerze|

## <a name="microsoftstorage"></a>Microsoft.Storage

| Operacja | Opis |
|---|---|
|/ register/działania|Rejestruje subskrypcję dostawcy zasobów magazynu hello hello i umożliwia tworzenie hello kont magazynu.|
|/checknameavailability/Read|Sprawdza, czy nazwa konta jest prawidłowa i czy nie jest używana.|
|/ storageAccounts/zapisu|Tworzy konto magazynu z hello określone parametry lub aktualizacji hello właściwości bądź tagi albo dodaje niestandardowy domenę hello określono konto magazynu.|
|/storageAccounts/DELETE|Usuwa istniejące konto magazynu.|
|/storageAccounts/listkeys/Action|Zwraca klucze dostępu hello hello określone konto magazynu.|
|/storageAccounts/regeneratekey/Action|Klucze dostępu hello odtwarza hello określone konto magazynu.|
|/storageAccounts/Read|Zwraca hello listę kont magazynu lub pobiera właściwości hello hello określone konto magazynu.|
|/storageAccounts/listAccountSas/Action|Zwraca token sygnatury dostępu Współdzielonego konta hello hello określone konto magazynu.|
|/storageAccounts/listServiceSas/Action|Token sygnatury dostępu Współdzielonego usługi magazynu|
|/storageAccounts/Services/diagnosticSettings/Write|Tworzenie/aktualizowanie ustawień diagnostycznych na konto magazynu.|
|/skus/Read|Wyświetla listę hello jednostki SKU obsługiwana przez Microsoft.Storage.|
|/Usages/Read|Zwraca hello limit i hello bieżącą liczbę użyć dla zasobów w hello określonej subskrypcji|
|/Operations/Read|Ankiety hello stan operacji asynchronicznej.|
|/Locations/deleteVirtualNetworkOrSubnets/Action|Powiadamia Microsoft.Storage, że trwa usuwanie wirtualnej sieci lub podsieci|

## <a name="microsoftstorsimple"></a>Microsoft.StorSimple

| Operacja | Opis |
|---|---|
|/managers/clearAlerts/Action|Wyczyść wszystkie alerty hello skojarzony z Menedżerem urządzeń hello.|
|/managers/getActivationKey/Action|Pobierz klucz aktywacji hello Menedżer urządzeń.|
|/managers/regenerateActivationKey/Action|Ponowne generowanie klucza aktywacji hello Menedżer urządzeń.|
|/managers/regenarateRegistationCertificate/Action|Ponowne tworzenie certyfikatu rejestracji dla menedżerów urządzeń hello.|
|/managers/getEncryptionKey/Action|Pobierz klucz szyfrowania hello Menedżer urządzeń.|
|/managers/Read|Wyświetla listę lub pobiera hello menedżerów urządzeń|
|/managers/DELETE|Usuwa hello menedżerów urządzeń|
|/ menedżerów/zapisu|Utwórz lub zaktualizuj hello menedżerów urządzeń|
|/managers/configureDevice/Action|Konfiguruje urządzenia|
|/managers/listActivationKey/Action|Pobiera klucz aktywacji hello hello Menedżera urządzeń StorSimple.|
|/managers/listPublicEncryptionKey/Action|Lista kluczy szyfrowania publicznego z Menedżera urządzeń StorSimple.|
|/managers/listPrivateEncryptionKey/Action|Pobiera klucz prywatny szyfrowania dla Menedżera urządzeń StorSimple.|
|/managers/provisionCloudAppliance/Action|Utwórz nowe urządzenia chmury.|
|Menedżerowie/zapisu|Operacja Utwórz magazyn tworzy zasób platformy Azure typu „magazyn”|
|Menedżerowie/odczytu|Witaj operacji Get magazynu pobiera obiekt reprezentujący hello zasobów platformy Azure typu "magazynu"|
|/ Menedżerów/usuwania|Witaj usunąć magazyn operacji usunięcia Witaj określony zasobów platformy Azure typu "magazynu"|
|/managers/storageAccountCredentials/Write|Utwórz lub zaktualizuj poświadczenia konta magazynu hello|
|/managers/storageAccountCredentials/Read|Wyświetla listę lub pobiera poświadczeń konta magazynu hello|
|/managers/storageAccountCredentials/DELETE|Usuwa poświadczenia konta magazynu hello|
|/managers/storageAccountCredentials/listAccessKey/Action|Listy kluczy dostępu do poświadczeń konta magazynu|
|/managers/accessControlRecords/Read|Wyświetla listę lub pobiera rekordy kontroli dostępu hello|
|/managers/accessControlRecords/Write|Utwórz lub zaktualizuj rekordy kontroli dostępu hello|
|/managers/accessControlRecords/DELETE|Usuwa rekordy kontroli dostępu hello|
|/managers/Metrics/Read|Wyświetla listę lub pobiera hello metryk|
|/managers/bandwidthSettings/Read|Wyświetl listę ustawień przepustowości hello (8000 serii tylko)|
|/managers/bandwidthSettings/Write|Tworzy nowy lub aktualizuje ustawienia przepustowości (8000 serii tylko)|
|/managers/bandwidthSettings/DELETE|Usuwa istniejące ustawienia przepustowości (8000 serii tylko)|
|Menedżerowie/extendedInformation/odczytu|Hello operacji Get Info rozszerzony pobiera obiekt rozszerzone informacje o reprezentujący hello zasobów platformy Azure typu? magazynu?|
|Menedżerowie/extendedInformation/zapisu|Hello operacji Get Info rozszerzony pobiera obiekt rozszerzone informacje o reprezentujący hello zasobów platformy Azure typu? magazynu?|
|/ Menedżerów/extendedInformation/usuwania|Hello operacji Get Info rozszerzony pobiera obiekt rozszerzone informacje o reprezentujący hello zasobów platformy Azure typu? magazynu?|
|/managers/Alerts/Read|Wyświetla listę lub pobiera hello alertów|
|/managers/storageDomains/Read|Wyświetla listę lub pobiera hello magazynu domen|
|/managers/storageDomains/Write|Utwórz lub zaktualizuj hello magazynu domen|
|/managers/storageDomains/DELETE|Usuwa hello magazynu domen|
|/managers/Devices/scanForUpdates/Action|Skanowanie w poszukiwaniu aktualizacji na urządzeniu.|
|/managers/Devices/Download/Action|Pobierania aktualizacji dla urządzenia.|
|/managers/Devices/Install/Action|Zainstaluj aktualizacje na urządzeniu.|
|/managers/Devices/Read|Wyświetla listę lub pobiera hello urządzeń|
|/managers/Devices/Write|Utwórz lub zaktualizuj hello urządzeń|
|/managers/Devices/DELETE|Usuwa hello urządzenia|
|/managers/Devices/Deactivate/Action|Dezaktywuje urządzenia.|
|/managers/Devices/publishSupportPackage/Action|Publikowanie pakietu obsługi urządzenia do firmy Microsoft Support rozwiązywania problemów.|
|/managers/Devices/Failover/Action|Tryb pracy awaryjnej hello urządzenia.|
|/managers/Devices/sendTestAlertEmail/Action|Wyślij testową wiadomość e-mail alertów tooconfigured adresatów wiadomości e-mail.|
|/managers/Devices/installUpdates/Action|Instaluje aktualizacje na urządzeniach hello|
|/managers/Devices/listFailoverSets/Action|Tryb failover hello listy ustawia istniejące urządzenie.|
|/managers/Devices/listFailoverTargets/Action|Cele trybu failover listy hello urządzeń|
|/managers/Devices/publicEncryptionKey/Action|Lista publicznego klucza szyfrowania hello Menedżera urządzeń|
|/ Menedżera urządzeń/hardwareComponentGroups /<br>Odczyt|Witaj listy grup składników sprzętowych|
|/ Menedżera urządzeń/hardwareComponentGroups /<br>changeControllerPowerState/działania|Zmiany stanu zasilania kontrolera grup składników sprzętowych|
|/managers/Devices/Metrics/Read|Wyświetla listę lub pobiera hello metryk|
|/managers/Devices/chapSettings/Write|Utwórz lub zaktualizuj ustawienia protokołu Chap hello|
|/managers/Devices/chapSettings/Read|Wyświetla listę lub pobiera hello ustawienia protokołu Chap|
|/managers/Devices/chapSettings/DELETE|Usuwa hello ustawienia protokołu Chap|
|/managers/Devices/backupScheduleGroups/Read|Wyświetla listę lub pobiera grup harmonogramu tworzenia kopii zapasowej hello|
|/managers/Devices/backupScheduleGroups/Write|Utwórz lub zaktualizuj grupy harmonogramu tworzenia kopii zapasowej hello|
|/managers/Devices/backupScheduleGroups/DELETE|Usuwa grupy harmonogram tworzenia kopii zapasowej hello|
|/managers/Devices/updateSummary/Read|Wyświetla listę lub pobiera hello aktualizacji — podsumowanie|
|/ Menedżera urządzeń/migrationSourceConfigurations /<br>Import/działania|Importowanie konfiguracji źródłowego do migracji|
|/ Menedżera urządzeń/migrationSourceConfigurations /<br>startMigrationEstimate/działania|Uruchom zadanie tooestimate hello czas trwania procesu migracji hello.|
|/ Menedżera urządzeń/migrationSourceConfigurations /<br>startMigration/działania|Uruchom migrację za pomocą konfiguracji źródła|
|/ Menedżera urządzeń/migrationSourceConfigurations /<br>confirmMigration/działania|Potwierdza udanej migracji, a następnie przekazać go.|
|/ Menedżera urządzeń/migrationSourceConfigurations /<br>fetchMigrationEstimate/działania|Pobierz stan zadania oceny migracji hello hello.|
|/ Menedżera urządzeń/migrationSourceConfigurations /<br>fetchMigrationStatus/działania|Pobierz stan hello hello migracji.|
|/ Menedżera urządzeń/migrationSourceConfigurations /<br>fetchConfirmMigrationStatus/działania|Upewnij się, hello pobierania stanu migracji.|
|/managers/Devices/alertSettings/Read|Wyświetla listę lub pobiera hello ustawienia alertu|
|/managers/Devices/alertSettings/Write|Utwórz lub zaktualizuj ustawienia alertu hello|
|/managers/Devices/networkSettings/Read|Wyświetla listę lub pobiera hello ustawień sieci|
|/managers/Devices/networkSettings/Write|Tworzy nowy lub aktualizuje ustawienia sieci|
|/managers/Devices/Jobs/Read|Wyświetla listę lub pobiera hello zadania|
|/managers/Devices/Jobs/Cancel/Action|Anuluj uruchomione zadania|
|/managers/Devices/metricsDefinitions/Read|Wyświetla listę lub pobiera definicje metryk hello|
|/managers/Devices/volumeContainers/Write|Tworzy nowy lub aktualizuje kontenery woluminów (8000 serii tylko)|
|/managers/Devices/volumeContainers/Read|Lista hello kontenery woluminów (8000 serii tylko)|
|/managers/Devices/volumeContainers/DELETE|Usuwa istniejące kontenery woluminów (8000 serii tylko)|
|/managers/Devices/volumeContainers/listEncryptionKeys/Action|Lista kluczy szyfrowania woluminu kontenerów|
|/managers/Devices/volumeContainers/rolloverEncryptionKey/Action|Klucze szyfrowania przerzucania kontenery woluminów|
|/managers/Devices/volumeContainers/Metrics/Read|Lista hello metryk|
|/managers/Devices/volumeContainers/Volumes/Read|Lista hello woluminów|
|/managers/Devices/volumeContainers/Volumes/Write|Tworzy nowy lub aktualizuje woluminów|
|/managers/Devices/volumeContainers/Volumes/DELETE|Usuwa istniejące woluminy|
|/managers/Devices/volumeContainers/Volumes/Metrics/Read|Lista hello metryk|
|/managers/Devices/volumeContainers/Volumes/metricsDefinitions/Read|Witaj listy definicji metryk|
|/managers/Devices/volumeContainers/metricsDefinitions/Read|Witaj listy definicji metryk|
|/managers/Devices/iscsiservers/Read|Wyświetla listę lub pobiera hello iSCSI serwerów|
|/managers/Devices/iscsiservers/Write|Utwórz lub zaktualizuj hello iSCSI serwerów|
|/managers/Devices/iscsiservers/DELETE|Usuwa hello iSCSI serwerów|
|/managers/Devices/iscsiservers/Backup/Action|Pobierz kopię zapasową serwera iSCSI.|
|/managers/Devices/iscsiservers/Metrics/Read|Wyświetla listę lub pobiera hello metryk|
|/managers/Devices/iscsiservers/Disks/Read|Wyświetla listę lub pobiera hello dysków|
|/managers/Devices/iscsiservers/Disks/Write|Utwórz lub zaktualizuj hello dysków|
|/managers/Devices/iscsiservers/Disks/DELETE|Usuwa hello dysków|
|/managers/Devices/iscsiservers/Disks/Metrics/Read|Wyświetla listę lub pobiera hello metryk|
|/managers/Devices/iscsiservers/Disks/metricsDefinitions/Read|Wyświetla listę lub pobiera definicje metryk hello|
|/managers/Devices/iscsiservers/metricsDefinitions/Read|Wyświetla listę lub pobiera definicje metryk hello|
|/managers/Devices/Backups/Read|Wyświetla listę lub pobiera hello zestawu kopii zapasowych|
|/managers/Devices/Backups/DELETE|Usuwa hello zestawu kopii zapasowych|
|/managers/Devices/Backups/Restore/Action|Przywróć wszystkie woluminy hello z zestawu kopii zapasowych.|
|/managers/Devices/Backups/Elements/clone/Action|Klonowanie udziale lub woluminie przy użyciu kopii zapasowej elementu.|
|/managers/Devices/backupPolicies/Write|Tworzy nowy lub aktualizuje zasady tworzenia kopii zapasowej (8000 serii tylko)|
|/managers/Devices/backupPolicies/Read|Zasady tworzenia kopii zapasowej hello listy (8000 serii tylko)|
|/managers/Devices/backupPolicies/DELETE|Usuwa istniejące zasady tworzenia kopii zapasowej (8000 serii tylko)|
|/managers/Devices/backupPolicies/Backup/Action|Podjąć kopii zapasowych wszystkich woluminów hello chronione przez zasady hello ręczne toocreate kopii zapasowej na żądanie.|
|/managers/Devices/backupPolicies/Schedules/Write|Tworzy nowy lub aktualizuje harmonogramów|
|/managers/Devices/backupPolicies/Schedules/Read|Harmonogramy hello listy|
|/managers/Devices/backupPolicies/Schedules/DELETE|Usuwa istniejących harmonogramów|
|/managers/Devices/securitySettings/Update/Action|Zaktualizuj ustawienia zabezpieczeń hello.|
|/managers/Devices/securitySettings/Read|Lista hello ustawienia zabezpieczeń|
|/ Menedżera urządzeń/securitySettings /<br>syncRemoteManagementCertificate/działania|Synchronizuj hello certyfikat zdalnego zarządzania dla urządzenia.|
|/managers/Devices/securitySettings/Write|Tworzy nowy lub aktualizuje ustawienia zabezpieczeń|
|/managers/Devices/fileservers/Read|Wyświetla listę lub pobiera hello serwerów plików|
|/managers/Devices/fileservers/Write|Utwórz lub zaktualizuj hello serwerów plików|
|/managers/Devices/fileservers/DELETE|Usuwa hello serwerów plików|
|/managers/Devices/fileservers/Backup/Action|Pobierz kopię zapasową serwera plików.|
|/managers/Devices/fileservers/Metrics/Read|Wyświetla listę lub pobiera hello metryk|
|/managers/Devices/fileservers/shares/Write|Utwórz lub zaktualizuj udziałów hello|
|/managers/Devices/fileservers/shares/Read|Wyświetla listę lub pobiera udziałów hello|
|/managers/Devices/fileservers/shares/DELETE|Usuwa udziałów hello|
|/managers/Devices/fileservers/shares/Metrics/Read|Wyświetla listę lub pobiera hello metryk|
|/managers/Devices/fileservers/shares/metricsDefinitions/Read|Wyświetla listę lub pobiera definicje metryk hello|
|/managers/Devices/fileservers/metricsDefinitions/Read|Wyświetla listę lub pobiera definicje metryk hello|
|/managers/Devices/timeSettings/Read|Wyświetla listę lub pobiera ustawienia czasu hello|
|/managers/Devices/timeSettings/Write|Tworzy nowy lub aktualizuje ustawienia czasu|
|Menedżerowie/certyfikatów/zapisu|Hello operacja aktualizacji zasobów certyfikatu aktualizuje certyfikat poświadczeń hello zasobów/magazynu.|
|/managers/cloudApplianceConfigurations/Read|Lista hello chmury urządzenia obsługiwane konfiguracje|
|/managers/metricsDefinitions/Read|Wyświetla listę lub pobiera definicje metryk hello|
|/managers/encryptionSettings/Read|Wyświetla listę lub pobiera hello ustawienia szyfrowania|

## <a name="microsoftstreamanalytics"></a>Microsoft.StreamAnalytics

| Operacja | Opis |
|---|---|
|/streamingjobs/Start/Action|Uruchom zadania usługi analiza strumienia|
|/streamingjobs/Stop/Action|Zatrzymanie zadania usługi analiza strumienia|
|/ streamingjobs/odczytu|Zadania usługi analiza strumienia odczytu|
|/ streamingjobs/zapisu|Zapis zadania usługi analiza strumienia|
|/ streamingjobs/Delete|Usuwanie zadania usługi analiza strumienia|
|/streamingjobs/Providers/Microsoft.Insights/metricDefinitions/Read|Pobiera dostępne metryki hello streamingjobs|
|/streamingjobs/Providers/Microsoft.Insights/diagnosticSettings/Read|Ustawienie diagnostyczne dla odczytu.|
|/streamingjobs/Providers/Microsoft.Insights/diagnosticSettings/Write|Zapis ustawienie diagnostyczne.|
|/streamingjobs/Providers/Microsoft.Insights/logDefinitions/Read|Pobiera dostępne dzienniki hello streamingjobs|
|/streamingjobs/Transformations/Read|Odczyt Stream Analytics zadania przekształcania|
|/streamingjobs/Transformations/Write|Zapis przekształcenie zadania usługi analiza strumienia|
|/streamingjobs/Transformations/DELETE|Usuń przekształcenie zadania usługi analiza strumienia|
|/streamingjobs/inputs/Read|Wejścia zadania usługi analiza strumienia odczytu|
|/streamingjobs/inputs/Write|Zapisu danych wejściowych zadania usługi analiza strumienia|
|/streamingjobs/inputs/DELETE|Usuń dane wejściowe zadania usługi analiza strumienia|
|/streamingjobs/outputs/Read|Odczytu Stream Analytics — dane wyjściowe zadania|
|/streamingjobs/outputs/Write|Zapisywania danych wyjściowych zadania usługi analiza strumienia|
|/streamingjobs/outputs/DELETE|Usuń dane wyjściowe zadania usługi analiza strumienia|

## <a name="microsoftsupport"></a>Microsoft.Support

| Operacja | Opis |
|---|---|
|/ register/działania|Rejestruje tooSupport dostawcy zasobów|
|/supportTickets/Read|Pobiera szczegóły biletu pomocy technicznej (w tym stan, ważność, szczegóły dotyczące kontaktu i komunikacji) lub pobiera hello listę biletów pomocy technicznej w subskrypcjach.|
|/ supportTickets/zapisu|Tworzy lub aktualizuje bilet pomocy technicznej. Można utworzyć biletu pomocy technicznej dla technicznych, rozliczeń, limity przydziału lub zarządzaniem subskrypcjami problemy związane z. Możesz zaktualizować ważność, szczegóły dotyczące kontaktu i komunikacji dla istniejących biletów pomocy technicznej.|

## <a name="microsoftweb"></a>Microsoft.Web

| Operacja | Opis |
|---|---|
|/ unregister/działania|Wyrejestrowanie dostawcy zasobów Microsoft.Web hello subskrypcji.|
|Zweryfikuj/działania|Sprawdzanie poprawności.|
|/ register/działania|Rejestrowanie dostawcy zasobów Microsoft.Web hello subskrypcji.|
|/ hostingEnvironments/odczytu|Pobierz właściwości hello środowiska usługi aplikacji|
|/ hostingEnvironments/zapisu|Tworzenie nowego środowiska usługi aplikacji lub zaktualizować istniejący|
|/ hostingEnvironments/Delete|Usuwanie środowiska usługi aplikacji|
|/hostingEnvironments/reboot/Action|Ponownie wszystkie maszyny w środowisku usługi aplikacji|
|/hostingenvironments/resume/Action|Wznów środowiskach hostingu.|
|/hostingenvironments/suspend/Action|Wstrzymaj środowiskach hostingu.|
|/hostingenvironments/metricdefinitions/Read|Pobierz Hosting definicji metryk środowisk.|
|/hostingEnvironments/workerPools/Read|Pobierz właściwości hello puli procesów roboczych w środowisku usługi aplikacji|
|/hostingEnvironments/workerPools/Write|Tworzenie nowej puli procesów roboczych w środowisku usługi aplikacji lub zaktualizuj istniejącą|
|/hostingenvironments/workerpools/metricdefinitions/Read|Pobierz Hosting definicje Metryka Workerpools środowisk.|
|/hostingenvironments/workerpools/Metrics/Read|Pobierz Hosting środowisk Workerpools metryki.|
|/hostingenvironments/workerpools/skus/Read|Pobierz Hosting jednostki SKU Workerpools środowisk.|
|/hostingenvironments/workerpools/Usages/Read|Pobierz Hosting środowisk Workerpools użycia.|
|/hostingenvironments/Sites/Read|Pobierz aplikacje sieci Web środowiskach hostingu.|
|/hostingenvironments/serverfarms/Read|Pobierz Hosting środowisk planów usługi aplikacji.|
|/hostingenvironments/Usages/Read|Pobierz Hosting użycia środowiska.|
|/hostingenvironments/capacities/Read|Pobierz Hosting możliwości środowiska.|
|/hostingenvironments/Operations/Read|Pobierz Hosting operacji środowisk.|
|/hostingEnvironments/multiRolePools/Read|Pobierz właściwości hello puli frontonu w środowisku usługi aplikacji|
|/hostingEnvironments/multiRolePools/Write|Tworzenie nowej puli frontonu w środowisku usługi aplikacji lub zaktualizuj istniejącą|
|/hostingenvironments/multirolepools/metricdefinitions/Read|Pobierz Hosting definicji metryk pełniących wiele pul środowisk.|
|/hostingenvironments/multirolepools/Metrics/Read|Pobierz Hosting środowisk pełniących wiele pul metryki.|
|/hostingenvironments/multirolepools/skus/Read|Pobierz Hosting jednostki SKU pełniących wiele pul środowisk.|
|/hostingenvironments/multirolepools/Usages/Read|Pobierz Hosting środowisk pełniących wiele pul użycia.|
|/hostingenvironments/Diagnostics/Read|Pobierz Hosting środowisk diagnostyki.|
|/publishingusers/Read|Pobierz publikowanie użytkowników.|
|/ publishingusers/zapisu|Aktualizacja publikowania użytkowników.|
|/checknameavailability/Read|Sprawdź, czy nazwa zasobu jest dostępna.|
|/ geoRegions/odczytu|Pobierz listę hello regionów geograficznych.|
|/ lokacji/odczytu|Pobierz właściwości hello aplikacji sieci Web|
|/ lokacji/zapisu|Utwórz nową aplikację sieci Web lub zaktualizuj istniejącą|
|/ lokacji/Delete|Usuń istniejącą aplikację sieci Web|
|/Sites/Backup/Action|Utwórz nową kopię zapasową aplikacji sieci web|
|/Sites/publishxml/Action|Pobierz publikowania format xml profilu dla aplikacji sieci Web|
|/Sites/publish/Action|Publikowanie aplikacji sieci Web|
|/Sites/restart/Action|Ponowne uruchomienie aplikacji sieci Web|
|/Sites/Start/Action|Uruchamiają aplikację sieci Web|
|/Sites/Stop/Action|Zatrzymać aplikacji sieci Web|
|/Sites/slotsswap/Action|Zamienić miejsc wdrażania aplikacji sieci Web|
|/Sites/slotsdiffs/Action|Pobierz różnic w konfiguracji aplikacji sieci web i gniazd|
|/Sites/applySlotConfig/Action|Zastosuj konfigurację miejsca aplikacji sieci web z docelowego miejsca toohello bieżącej aplikacji sieci web|
|/Sites/resetSlotConfig/Action|Zresetuj konfigurację aplikacji sieci web|
|/Sites/Functions/Action|Funkcje aplikacji sieci Web.|
|/Sites/listsyncfunctiontriggerstatus/Action|Lista synchronizacji funkcja wyzwalacz stanu aplikacji sieci Web.|
|/Sites/networktrace/Action|Aplikacje sieci Web śledzenia sieci.|
|/Sites/newpassword/Action|Aplikacje sieci Web NoweHasło.|
|/Sites/Sync/Action|Aplikacje sieci Web synchronizacji.|
|/Sites/operationresults/Read|Pobierz wyniki operacji aplikacji sieci Web.|
|/Sites/webjobs/Read|Pobrania zadań Webjob aplikacji sieci Web.|
|/ lokacji/tworzenia kopii zapasowej/odczytu|Pobierz kopii zapasowej aplikacji sieci Web.|
|/Sites/Backup/Write|Aktualizacja kopii zapasowej aplikacji sieci Web.|
|/Sites/metricdefinitions/Read|Pobierz definicje Metryka aplikacji sieci Web.|
|/Sites/Metrics/Read|Pobieraj metryki aplikacji sieci Web.|
|/Sites/continuouswebjobs/DELETE|Usuń zadania ciągłego sieci Web aplikacji sieci Web.|
|/Sites/continuouswebjobs/Read|Pobierz zadania ciągłego sieci Web aplikacji sieci Web.|
|/Sites/continuouswebjobs/Start/Action|Rozpocznij zadania ciągłego sieci Web aplikacji sieci Web.|
|/Sites/continuouswebjobs/Stop/Action|Zatrzymanie zadania ciągłego sieci Web aplikacji sieci Web.|
|/Sites/domainownershipidentifiers/Read|Pobierz identyfikatory własność domeny aplikacji sieci Web.|
|/Sites/domainownershipidentifiers/Write|Zaktualizuj identyfikatory własność domeny aplikacji sieci Web.|
|/Sites/premieraddons/DELETE|Usuń dodatków Premier aplikacji sieci Web.|
|/Sites/premieraddons/Read|Pobierz dodatki Premier aplikacji sieci Web.|
|/Sites/premieraddons/Write|Aktualizowanie dodatków Premier aplikacji sieci Web.|
|/Sites/triggeredwebjobs/DELETE|Usuń wyzwalanych zadań Webjob aplikacji sieci Web.|
|/Sites/triggeredwebjobs/Read|Pobierz wyzwalanych zadań Webjob aplikacji sieci Web.|
|/Sites/triggeredwebjobs/Run/Action|Uruchom wyzwalanych zadań Webjob aplikacji sieci Web.|
|/Sites/hostnamebindings/DELETE|Usuń powiązania nazwę hosta aplikacji sieci Web.|
|/Sites/hostnamebindings/Read|Pobierz powiązania nazwę hosta aplikacji sieci Web.|
|/Sites/hostnamebindings/Write|Zaktualizuj powiązania nazwę hosta aplikacji sieci Web.|
|/Sites/virtualnetworkconnections/DELETE|Usuwanie połączenia wirtualnej sieci aplikacji sieci Web.|
|/Sites/virtualnetworkconnections/Read|Pobrać połączeń sieci wirtualnej aplikacji sieci Web.|
|/Sites/virtualnetworkconnections/Write|Zaktualizuj połączenia wirtualnej sieci aplikacji sieci Web.|
|/Sites/virtualnetworkconnections/Gateways/Read|Pobierz bram połączeń sieci wirtualnej aplikacji sieci Web.|
|/Sites/virtualnetworkconnections/Gateways/Write|Zaktualizuj bramy połączenia wirtualnej sieci aplikacji sieci Web.|
|/Sites/publishxml/Read|Pobierz aplikacje sieci Web publikowanie XML.|
|/Sites/hybridconnectionrelays/Read|Pobierz przekaźników połączeń hybrydowych aplikacji sieci Web.|
|/Sites/perfcounters/Read|Pobierz liczniki wydajności aplikacji sieci Web.|
|/Sites/Usages/Read|Pobierz użycia aplikacji sieci Web.|
|/Sites/Slots/Write|Utwórz nowe miejsce aplikacji sieci Web lub zaktualizuj istniejącą|
|/Sites/Slots/DELETE|Usuwanie istniejącego miejsca aplikacji sieci Web|
|/Sites/Slots/Backup/Action|Utwórz nową kopię zapasową miejsca aplikacji sieci Web.|
|/Sites/Slots/publishxml/Action|Pobierz publikowanie format xml profilu dla miejsca aplikacji sieci Web|
|/Sites/Slots/publish/Action|Publikowanie miejsca aplikacji sieci Web|
|/Sites/Slots/restart/Action|Uruchom ponownie miejsca aplikacji sieci Web|
|/Sites/Slots/Start/Action|Uruchom miejsca aplikacji sieci Web|
|/Sites/Slots/Stop/Action|Zatrzymaj miejsca aplikacji sieci Web|
|/Sites/Slots/slotsswap/Action|Zamienić miejsc wdrażania aplikacji sieci Web|
|/Sites/Slots/slotsdiffs/Action|Pobierz różnic w konfiguracji aplikacji sieci web i gniazd|
|/Sites/Slots/applySlotConfig/Action|Zastosuj konfigurację miejsca aplikacji sieci web z poziomu gniazda bieżącego toohello miejsca docelowego.|
|/Sites/Slots/resetSlotConfig/Action|Zresetuj konfigurację miejsca aplikacji sieci web|
|/Sites/Slots/Read|Pobierz właściwości hello miejsce wdrożenia aplikacji sieci Web|
|/Sites/Slots/newpassword/Action|Miejsc aplikacji sieci Web NoweHasło.|
|/Sites/Slots/Sync/Action|Synchronizacja miejsc aplikacji sieci Web.|
|/Sites/Slots/operationresults/Read|Pobierz wyniki operacji miejsc aplikacji sieci Web.|
|/Sites/Slots/webjobs/Read|Uzyskać zadań Webjob miejsc aplikacji sieci Web.|
|/Sites/Slots/Backup/Write|Zaktualizuj kopii zapasowej miejsc aplikacji sieci Web.|
|/Sites/Slots/metricdefinitions/Read|Pobierz definicje metryk miejsc aplikacji sieci Web.|
|/Sites/Slots/Metrics/Read|Pobieraj metryki miejsc aplikacji sieci Web.|
|/Sites/Slots/continuouswebjobs/DELETE|Usuń zadania ciągłego Web miejsc aplikacji sieci Web.|
|/Sites/Slots/continuouswebjobs/Read|Pobierz zadania ciągłego Web miejsc aplikacji sieci Web.|
|/Sites/Slots/continuouswebjobs/Start/Action|Uruchom zadania ciągłego Web miejsc aplikacji sieci Web.|
|/Sites/Slots/continuouswebjobs/Stop/Action|Zatrzymanie zadania ciągłego Web miejsc aplikacji sieci Web.|
|/Sites/Slots/premieraddons/DELETE|Usuń dodatków Premier miejsc aplikacji sieci Web.|
|/Sites/Slots/premieraddons/Read|Pobierz dodatki Premier miejsc aplikacji sieci Web.|
|/Sites/Slots/premieraddons/Write|Zaktualizuj dodatków Premier miejsc aplikacji sieci Web.|
|/Sites/Slots/triggeredwebjobs/DELETE|Usuwanie zadań Webjob wyzwalanych miejsc aplikacji sieci Web.|
|/Sites/Slots/triggeredwebjobs/Read|Pobrania zadań Webjob wyzwalanych miejsc aplikacji sieci Web.|
|/Sites/Slots/triggeredwebjobs/Run/Action|Uruchamianie zadań Webjob wyzwalanych miejsc aplikacji sieci Web.|
|/Sites/Slots/hostnamebindings/DELETE|Usuń powiązań z nazwami hostów miejsc aplikacji sieci Web.|
|/Sites/Slots/hostnamebindings/Read|Pobierz powiązań z nazwami hostów miejsc aplikacji sieci Web.|
|/Sites/Slots/hostnamebindings/Write|Zaktualizować powiązań z nazwami hostów miejsc aplikacji sieci Web.|
|/Sites/Slots/phplogging/Read|Pobierz Phplogging miejsc aplikacji sieci Web.|
|/Sites/Slots/virtualnetworkconnections/DELETE|Usuwanie połączenia wirtualnej sieci miejsc aplikacji sieci Web.|
|/Sites/Slots/virtualnetworkconnections/Read|Pobierz połączenia wirtualnej sieci miejsc aplikacji sieci Web.|
|/Sites/Slots/virtualnetworkconnections/Write|Zaktualizuj połączenia wirtualnych sieci miejsc aplikacji sieci Web.|
|/Sites/Slots/virtualnetworkconnections/Gateways/Write|Zaktualizuj bramy połączeń sieci wirtualnej miejsc aplikacji sieci Web.|
|/Sites/Slots/Usages/Read|Pobierz użycia miejsc aplikacji sieci Web.|
|/Sites/Slots/hybridconnection/DELETE|Usuwanie połączenia hybrydowego miejsc aplikacji sieci Web.|
|/Sites/Slots/hybridconnection/Read|Pobierz połączenia hybrydowego miejsc aplikacji sieci Web.|
|/Sites/Slots/hybridconnection/Write|Zaktualizuj połączenie hybrydowe miejsc aplikacji sieci Web.|
|/Sites/Slots/config/Read|Pobierz ustawienia konfiguracji miejsca aplikacji sieci Web|
|/Sites/Slots/config/list/Action|Lista miejsca aplikacji sieci Web poufne ustawienia zabezpieczeń, takie jak publikowania poświadczeń, ustawienia aplikacji i parametry połączenia|
|/Sites/Slots/config/Write|Aktualizowanie ustawień konfiguracji miejsca aplikacji sieci Web|
|/Sites/Slots/config/DELETE|Usuwanie konfiguracji miejsc aplikacji sieci Web.|
|/Sites/Slots/instances/Read|Pobierz wystąpienia miejsc aplikacji sieci Web.|
|/Sites/Slots/instances/processes/Read|Pobierz procesów wystąpień miejsc aplikacji sieci Web.|
|/Sites/Slots/instances/Deployments/Read|Pobierz wdrożeń wystąpień miejsc aplikacji sieci Web.|
|/Sites/Slots/sourcecontrols/Read|Pobierz ustawienia konfiguracji miejsca aplikacji sieci Web do kontroli źródła|
|/Sites/Slots/sourcecontrols/Write|Zaktualizuj ustawienia konfiguracji kontroli źródła miejsca aplikacji sieci Web|
|/Sites/Slots/sourcecontrols/DELETE|Usuń ustawienia konfiguracji kontroli źródła miejsca aplikacji sieci Web|
|/Sites/Slots/Restore/Read|Pobierz przywracania miejsc aplikacji sieci Web.|
|/Sites/Slots/analyzecustomhostname/Read|Pobierz Web miejsc aplikacji analizowanie niestandardową nazwę hosta.|
|/Sites/Slots/Backups/Read|Pobierz właściwości hello kopii zapasowej miejsc aplikacji sieci web|
|/Sites/Slots/Backups/list/Action|Lista sieci Web aplikacji miejsc wykonywanie kopii zapasowych.|
|/Sites/Slots/Backups/Restore/Action|Przywracanie kopii zapasowych miejsc aplikacji sieci Web.|
|/Sites/Slots/Deployments/DELETE|Usunięcie wdrożeń miejsc aplikacji sieci Web.|
|/Sites/Slots/Deployments/Read|Pobierz wdrożeń miejsc aplikacji sieci Web.|
|/Sites/Slots/Deployments/Write|Zaktualizuj wdrożeń miejsc aplikacji sieci Web.|
|/Sites/Slots/Deployments/log/Read|Pobierz dziennik wdrożeń miejsc aplikacji sieci Web.|
|/Sites/hybridconnection/DELETE|Usuwanie połączenia hybrydowego aplikacji sieci Web.|
|/Sites/hybridconnection/Read|Pobierz dane o połączeniu hybrydowych aplikacji sieci Web.|
|/Sites/hybridconnection/Write|Zaktualizuj połączenie hybrydowe aplikacji sieci Web.|
|/Sites/recommendationhistory/Read|Pobierz historię zalecenie aplikacji sieci Web.|
|/Sites/recommendations/Read|Pobierz listę hello zalecenia dla aplikacji sieci web.|
|/Sites/recommendations/disable/Action|Wyłącz zalecenia dotyczące aplikacji sieci Web.|
|/Sites/config/Read|Pobierz ustawienia konfiguracji aplikacji sieci Web|
|/Sites/config/list/Action|Wyświetl listę aplikacji sieci Web poufne ustawienia zabezpieczeń, takie jak publikowania poświadczeń, ustawienia aplikacji i parametry połączenia|
|/Sites/config/Write|Zaktualizuj ustawienia konfiguracji aplikacji sieci Web|
|/Sites/config/DELETE|Usuwanie konfiguracji aplikacji sieci Web.|
|/Sites/instances/Read|Pobierz wystąpienia aplikacji sieci Web.|
|/Sites/instances/processes/DELETE|Usuń procesów wystąpienia aplikacji sieci Web.|
|/Sites/instances/processes/Read|Pobierz procesów wystąpienia aplikacji sieci Web.|
|/Sites/instances/Deployments/Read|Pobierz wdrożeń wystąpienia aplikacji sieci Web.|
|/Sites/sourcecontrols/Read|Pobierz ustawienia konfiguracji aplikacji sieci Web do kontroli źródła|
|/Sites/sourcecontrols/Write|Zaktualizuj ustawienia konfiguracji kontroli źródła dla aplikacji sieci Web|
|/Sites/sourcecontrols/DELETE|Usuń ustawienia konfiguracji kontroli źródła dla aplikacji sieci Web|
|/Sites/Restore/Read|Pobierz przywracania aplikacji sieci Web.|
|/Sites/analyzecustomhostname/Read|Przeanalizuj niestandardową nazwę hosta.|
|/Sites/Backups/Read|Pobierz właściwości hello kopii zapasowej aplikacji sieci web|
|/Sites/Backups/list/Action|Lista kopie zapasowe aplikacji sieci Web.|
|/Sites/Backups/Restore/Action|Przywracać kopie zapasowe aplikacji sieci Web.|
|/Sites/snapshots/Read|Pobrać migawek aplikacji sieci Web.|
|/Sites/Functions/DELETE|Usuń funkcje aplikacji sieci Web.|
|/Sites/Functions/listsecrets/Action|Listy kluczy tajnych funkcje aplikacji sieci Web.|
|/Sites/Functions/Read|Pobierz funkcje aplikacji sieci Web.|
|/Sites/Functions/Write|Zaktualizuj funkcje aplikacji sieci Web.|
|/Sites/Deployments/DELETE|Usunięcie wdrożenia aplikacji sieci Web.|
|/Sites/Deployments/Read|Pobierz wdrożenia aplikacji sieci Web.|
|/Sites/Deployments/Write|Aktualizacji wdrożenia aplikacji sieci Web.|
|/Sites/Deployments/log/Read|Pobierz dziennik wdrożenia aplikacji sieci Web.|
|/Sites/Diagnostics/Read|Pobierz diagnostyki aplikacji sieci Web.|
|/Sites/Diagnostics/workerprocessrecycle/Read|Pobierz odtworzenia procesu roboczego diagnostyki aplikacji sieci Web.|
|/Sites/Diagnostics/workeravailability/Read|Pobierz Workeravailability diagnostyki aplikacji sieci Web.|
|/Sites/Diagnostics/runtimeavailability/Read|Pobierz dostępności środowiska uruchomieniowego diagnostyki aplikacji sieci Web.|
|/Sites/Diagnostics/cpuanalysis/Read|Pobierz Cpuanalysis diagnostyki aplikacji sieci Web.|
|/Sites/Diagnostics/servicehealth/Read|Pobierz kondycję usługi sieci Web diagnostyki aplikacji.|
|/Sites/Diagnostics/frebanalysis/Read|Pobierz analizy FREB diagnostyki aplikacji sieci Web.|
|/availablestacks/Read|Pobierz stosy dostępne.|
|/isusernameavailable/Read|Sprawdź, czy nazwa użytkownika jest dostępna.|
|/Microsoft.Web/apiManagementAccounts/<br>interfejsy API odczytu|Pobierz listę hello interfejsów API.|
|/Microsoft.Web/apiManagementAccounts/<br>interfejsy API/zapisu|Dodaj nowy interfejs Api lub zaktualizować istniejący.|
|/Microsoft.Web/apiManagementAccounts/<br>interfejsy API/usuwania|Usuń istniejące interfejsu Api.|
|/Microsoft.Web/apiManagementAccounts/<br>interfejsy API połączeń/odczytu|Pobierz hello listę połączeń.|
|/Microsoft.Web/apiManagementAccounts/<br>interfejsy API i połączeń/zapisu|Zapisz nowe połączenie, lub zaktualizuj istniejącą.|
|/Microsoft.Web/apiManagementAccounts/<br>interfejsy API/połączeń/usuwania|Usuń istniejące połączenie.|
|/Microsoft.Web/apiManagementAccounts/<br>interfejsy API połączeń/connectionAcls/odczytu|ConnectionAcls odczytu|
|/Microsoft.Web/apiManagementAccounts/<br>interfejsy API i połączeń/connectionAcls/zapisu|Dodaj lub zaktualizuj ConnectionAcl|
|/Microsoft.Web/apiManagementAccounts/<br>interfejsy API/połączeń/connectionAcls/usuwania|Usuń ConnectionAcl|
|/Microsoft.Web/apiManagementAccounts/<br>interfejsy API connectionAcls/odczytu|ConnectionAcls odczytu dla interfejsu Api|
|/Microsoft.Web/apiManagementAccounts/<br>interfejsy API apiAcls/odczytu|ConnectionAcls odczytu|
|/Microsoft.Web/apiManagementAccounts/<br>interfejsy API i apiAcls/zapisu|Utwórz lub zaktualizuj interfejs Api listy kontroli dostępu|
|/Microsoft.Web/apiManagementAccounts/<br>interfejsy API/apiAcls/usuwania|Usuń listy ACL interfejsu Api|
|/ serverfarms/odczytu|Pobierz właściwości hello na Plan usługi App Service|
|/ serverfarms/zapisu|Tworzenie planu usługi aplikacji lub zaktualizuj istniejącą|
|/ serverfarms/Delete|Usuń istniejący Plan usługi App Service|
|/serverfarms/restartSites/Action|Uruchom ponownie wszystkie aplikacje sieci Web w planie usługi aplikacji|
|/serverfarms/operationresults/Read|Pobierz wyniki operacji planów usługi aplikacji.|
|/serverfarms/Capabilities/Read|Skorzystaj z możliwości planów usługi aplikacji.|
|/serverfarms/metricdefinitions/Read|Pobierz definicje metryki planów usługi aplikacji.|
|/serverfarms/Metrics/Read|Pobieraj metryki planów usługi aplikacji.|
|/serverfarms/hybridconnectionplanlimits/Read|Pobiera limity planu połączeń hybrydowych planów usługi aplikacji.|
|/serverfarms/virtualnetworkconnections/Read|Pobrać połączeń sieci wirtualnej planów usługi aplikacji.|
|/serverfarms/virtualnetworkconnections/Routes/DELETE|Usuń trasy połączenia wirtualnej sieci planów usługi aplikacji.|
|/serverfarms/virtualnetworkconnections/Routes/Read|Pobierz trasy połączenia wirtualnej sieci planów usługi aplikacji.|
|/serverfarms/virtualnetworkconnections/Routes/Write|Aktualizowanie tras połączenia wirtualnej sieci planów usługi aplikacji.|
|/serverfarms/virtualnetworkconnections/Gateways/Write|Zaktualizuj bramy połączenia wirtualnej sieci planów usługi aplikacji.|
|/serverfarms/firstpartyapps/Settings/DELETE|Usuń ustawienia aplikacje firm pierwszy planów usługi aplikacji.|
|/serverfarms/firstpartyapps/Settings/Read|Pobierz ustawienia aplikacje firm pierwszy planów usługi aplikacji.|
|/serverfarms/firstpartyapps/Settings/Write|Zaktualizuj ustawienia aplikacje firm pierwszy planów usługi aplikacji.|
|/serverfarms/Sites/Read|Pobierz aplikacje sieci Web planów usługi aplikacji.|
|/serverfarms/workers/reboot/Action|Ponowny rozruch pracowników planów usługi aplikacji.|
|/serverfarms/hybridconnectionrelays/Read|Pobierz przekaźników połączenia hybrydowe planów usługi aplikacji.|
|/serverfarms/skus/Read|Pobierz jednostki SKU planów usługi aplikacji.|
|/serverfarms/Usages/Read|Pobierz użycia planów usługi aplikacji.|
|/serverfarms/hybridconnectionnamespaces/relays/Sites/Read|Pobierz hybrydowego planów usługi aplikacji połączenia aplikacji sieci Web przekaźników przestrzeni nazw.|
|/ishostnameavailable/Read|Sprawdź, czy nazwa hosta jest dostępny.|
|/ connectionGateways/odczytu|Pobierz listę hello połączenia bramy.|
|/ connectionGateways/zapisu|Tworzy lub aktualizuje bramy połączenia.|
|/ connectionGateways/Delete|Usuwa bramę połączenia.|
|/connectionGateways/JOIN/Action|Tworzy sprzężenie bramy połączenia.|
|/classicmobileservices/Read|Pobierz klasycznego usług mobilnych.|
|/skus/Read|Pobierz jednostki SKU.|
|/ certyfikatów/odczytu|Pobierz listę hello certyfikatów.|
|/ certyfikatów/zapisu|Dodaj nowy certyfikat lub zaktualizuj istniejącą.|
|/ certyfikatów/Delete|Usuwanie istniejącego certyfikatu.|
|/Operations/Read|Pobierz operacje.|
|/ zalecenia/odczytu|Pobierz listę hello zalecenia dla subskrypcji.|
|/ishostingenvironmentnameavailable/Read|GET, jeśli jest dostępna nazwa środowiska hostingu.|
|/ apiManagementAccounts/odczytu|Pobierz listę hello ApiManagementAccounts.|
|/ apiManagementAccounts/zapisu|Dodaj nowy ApiManagementAccount lub zaktualizuj istniejącą|
|/ apiManagementAccounts/Delete|Usuń istniejące ApiManagementAccount|
|/apiManagementAccounts/connectionAcls/Read|Pobierz hello listę ACL połączenia.|
|/apiManagementAccounts/apiAcls/Read|ConnectionAcls odczytu|
|/ połączeń/odczytu|Pobierz hello listę połączeń.|
|/ połączeń/zapisu|Tworzy lub aktualizuje połączenia.|
|/ połączeń/Delete|Usuwa połączenie.|
|/Connections/JOIN/Action|Tworzy sprzężenie połączenia.|
|/Connections/confirmconsentcode/Action|Potwierdź kod zgody połączenia.|
|/Connections/listconsentlinks/Action|Lista łączy zgody dla połączeń.|
|/deploymentlocations/Read|Uzyskanie lokalizacji wdrożenia.|
|/sourcecontrols/Read|Pobierz kontroli źródła.|
|/ sourcecontrols/zapisu|Zaktualizuj kontrolki źródła.|
|/managedhostingenvironments/Read|Pobierz zarządzanych środowiskach hostingu.|
|/managedhostingenvironments/Sites/Read|Pobierz zarządzane Hosting aplikacji sieci Web środowiska.|
|/managedhostingenvironments/serverfarms/Read|Pobierz zarządzane Hosting środowisk planów usługi aplikacji.|
|/Locations/managedapis/Read|Pobierz lokalizacje zarządzanych interfejsów API.|
|/Locations/apioperations/Read|Pobierz operacje lokalizacje interfejsu API.|
|/Locations/connectiongatewayinstallations/Read|Pobierz lokalizacje połączenia bramy instalacji.|
|/ listSitesAssignedToHostName/odczytu|Pobierz nazwy lokacji przypisane toohostname.|

## <a name="next-steps"></a>Następne kroki

- Dowiedz się, jak za[utworzyć niestandardową rolę](role-based-access-control-custom-roles.md).

- Przejrzyj hello [wbudowane role RBAC](role-based-access-built-in-roles.md).

- Dowiedz się, jak toomanage uzyskują dostęp do przypisania [przez użytkownika](role-based-access-control-manage-assignments.md) lub [przez zasób](role-based-access-control-configure.md) 
