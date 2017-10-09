---
title: "aaaSupported typów zasobów za pośrednictwem kondycji zasobów platformy Azure | Dokumentacja firmy Microsoft"
description: "Obsługiwane typy zasobów za pośrednictwem kondycji zasobów platformy Azure"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 03/19/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: fc7bef214702f8ba6954b5aca62236b38023d27a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resource-types-and-health-checks-in-azure-resource-health"></a>Typy zasobów i kondycji sprawdza w kondycji zasobów platformy Azure
Poniżej znajduje się pełna lista wszystkich kontroli hello wykonywane za pośrednictwem kondycja zasobów przez typy zasobów.

## <a name="microsoftcacheredisredis"></a>Microsoft.CacheRedis/Redis
|Wykonanie testów|
|---|
|<ul><li>Są wszystkie węzły w pamięci podręcznej hello włączone i uruchomione?</li><li>Hello pamięci podręcznej jest osiągalna z wewnątrz centrum danych hello?</li><li>Ma powitalne pamięci podręcznej osiągnięto maksymalną liczbę połączeń hello?</li><li> Pamięć podręczna hello wyczerpała jego dostępnej pamięci? </li><li>Witaj pamięci podręcznej występują dużej liczby błędów stron?</li><li>Jest hello pamięci podręcznej duże obciążenie?</li></ul>|

## <a name="microsoftcdnprofile"></a>Microsoft.CDN/profile
|Wykonanie testów|
|---|
|<ul> <li>Wszelkie punkty końcowe hello została zatrzymana, usunięte lub jest niepoprawnie skonfigurowany?</li><li>Portalu dodatkowym hello jest niedostępny dla operacji konfiguracji sieci CDN?</li><li>Czy istnieją dostarczania bieżących problemów z hello punktów końcowych usługi CDN?</li><li>Użytkownicy, można zmienić konfiguracji hello z zasobami w sieci CDN?</li><li>Zmiany konfiguracji propagują szybkością hello oczekiwano?</li><li>Użytkownicy, można zarządzać przy użyciu hello portalu Azure, programu PowerShell lub interfejsu API hello konfiguracji CDN hello?</li> </ul>|

## <a name="microsoftclassiccomputevirtualmachines"></a>Microsoft.classiccompute/virtualmachines
|Wykonanie testów|
|---|
|<ul><li>Działa powitania serwera hosta, a następnie uruchomiona?</li><li>Rozruch systemu operacyjnego hosta hello ukończono?</li><li>Są udostępniane hello kontenera maszyny wirtualnej i włączone?</li><li>Czy istnieje połączenie sieciowe między hello hosta i konto magazynu hello?</li><li>Witaj rozruchu przez system operacyjny gościa hello ukończono?</li><li>Istnieje już uruchomione zaplanowanej konserwacji?</li></ul>|

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.cognitiveservices/accounts
|Wykonanie testów|
|---|
|<ul><li>Konto hello jest osiągalna z w obrębie centrum danych hello?</li><li>Jest hello kognitywnych dostawcy zasobów usługi dostępne?</li><li>Jest hello kognitywnych usługi dostępne w regionie odpowiednie hello?</li><li>Może być odczytany można wykonać operacji na koncie magazynu hello zawierający metadane zasobu hello?</li><li>Został osiągnięty limit przydziału wywołania hello interfejsu API?</li><li>Został osiągnięty limit odczytu wywołania hello interfejsu API?</li></ul>|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.COMPUTE/virtualmachines
|Wykonanie testów|
|---|
|<ul><li>Jest powitania serwera hostingu tej maszyny wirtualnej w górę i systemem?</li><li>Rozruch systemu operacyjnego hosta hello ukończono?</li><li>Są udostępniane hello kontenera maszyny wirtualnej i włączone?</li><li>Czy istnieje połączenie sieciowe między hello hosta i konto magazynu hello?</li><li>Witaj rozruchu przez system operacyjny gościa hello ukończono?</li><li>Istnieje już uruchomione zaplanowanej konserwacji?</li></ul>|

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.datalakeanalytics/accounts
|Wykonanie testów|
|---|
|<ul><li>Można użytkowników, których przesyłania zadania tooData Lake Analytics w hello region?</li><li>Czy podstawowe zadania hello wykonywania i ukończono pomyślnie w regionie?</li><li>Użytkownicy mogą listy elementów katalogu w regionie hello?</li>|


## <a name="microsoftdatalakestoreaccounts"></a>Microsoft.datalakestore/accounts
|Wykonanie testów|
|---|
|<ul><li>Użytkownicy, można przekazać danych tooData Lake Store w regionie hello?</li><li>Użytkownicy pobrać danych z usługi Data Lake Store w regionie hello?</li></ul>|

## <a name="microsoftdocumentdbdatabaseaccounts"></a>Microsoft.documentdb/databaseAccounts
|Wykonanie testów|
|---|
|<ul><li>Zostały jeszcze żądań bazy danych lub kolekcji nieobsługiwana z powodu niedostępności usługi DocumentDB tooa?</li><li>Nie ma w niej żądań dokumentu nieobsługiwana z powodu niedostępności usługi DocumentDB tooa?</li></ul>|

## <a name="microsoftnetworkconnections"></a>Microsoft.Network/Connections
|Wykonanie testów|
|---|
|<ul><li>Tunel VPN hello jest podłączony?</li><li>W związku z hello są konflikty konfiguracji?</li><li>Klucze wstępne hello poprawnie skonfigurowanych?</li><li>Urządzenia lokalnego VPN hello jest dostępny?</li><li>Zasady zabezpieczeń IPSec i IKE hello są niezgodności?</li><li>Czy połączenia sieci VPN S2S hello prawidłowo zainicjowana lub w stanie niepowodzenia?</li><li>Prawidłowo zainicjowana lub w stanie niepowodzenia, jest hello Wirtualnymi do połączenia?</li></ul>|

## <a name="microsoftnetworkvirtualnetworkgateways"></a>Microsoft.network/virtualNetworkGateways
|Wykonanie testów|
|---|
|<ul><li>Jest dostępny z bramy sieci VPN hello hello internet?</li><li>Jest hello bramy sieci VPN w trybie rezerwy?</li><li>Hello usługi sieci VPN jest uruchomiona w bramie hello?</li></ul>|

## <a name="microsoftnotificationhubsnamespace"></a>Microsoft.NotificationHubs/namespace
|Wykonanie testów|
|---|
|<ul><li> Środowisko uruchomieniowe operacje, takie jak rejestracji, instalacji lub wysyłania można wykonać na powitania przestrzeni nazw?</li></ul>|

## <a name="microsoftpowerbiworkspacecollections"></a>Microsoft.PowerBI/workspaceCollections
|Wykonanie testów|
|---|
|<ul><li>Zależy od systemu operacyjnego hosta hello i systemem?</li><li>Hello workspaceCollection jest dostępny z poza centrum danych hello?</li><li>Jest hello dostępne dostawcy zasobów usługi Power BI?</li><li>Jest hello dostępna usługa Power BI w regionie odpowiednie hello?</li></ul>|

## <a name="microsoftsearchsearchservices"></a>Microsoft.search/searchServices
|Wykonanie testów|
|---|
|<ul><li>Można wykonać operacji diagnostyki w klastrze hello?</li></ul>|

## <a name="microsoftsqlserverdatabase"></a>Microsoft.SQL/Server/database
|Wykonanie testów|
|---|
|<ul><li> Zostały logowania do bazy danych z toohello?</li></ul>|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs
|Wykonanie testów|
|---|
|<ul><li>Czy wszystkie hosty hello gdzie wykonywania zapasowej i uruchamiania zadania hello?</li><li>Został hello zadania toostart?</li><li>Czy istnieją bieżące środowisko uruchomieniowe uaktualnienia?</li><li>Zadanie hello w oczekiwanym stanem (np. uruchomiona lub zatrzymana przez klienta)?</li><li>Witaj zadania napotkał limit pamięci wyjątków?</li><li>Dostępne są aktualizacje trwającą obliczeń zaplanowane?</li><li>Jest hello menedżera wykonywania (plan kontroli) dostępne?</li></ul>|

## <a name="microsoftwebserverfarms"></a>Microsoft.web/serverFarms
|Wykonanie testów|
|---|
|<ul><li>Działa powitania serwera hosta, a następnie uruchomiona?</li><li>Internetowe usługi informacyjne jest uruchomiona?</li><li>Moduł równoważenia obciążenia hello jest uruchomiona?</li><li>Witaj planów usługi sieci Web jest osiągalna z w obrębie centrum danych hello?</li><li>Jest dostępna hello magazynu konta hostingu hello witryn zawartości dla hello serverFarm?</li></ul>|

## <a name="microsoftwebsites"></a>Microsoft.Web/Sites
|Wykonanie testów|
|---|
|<ul><li>Działa powitania serwera hosta, a następnie uruchomiona?</li><li>Internet Information server jest uruchomiona?</li><li>Moduł równoważenia obciążenia hello jest uruchomiona?</li><li>Hello aplikacji sieci Web jest osiągalna z wewnątrz centrum danych hello?</li><li>Konto magazynu hello uruchomiono hello dostępnej zawartości witryny?</li></ul>|

# <a name="next-steps"></a>Następne kroki
-  Zobacz [tooAzure wprowadzenie kondycja usługi](service-health-overview.md) i [tooAzure wprowadzenie kondycja zasobów](resource-health-overview.md) toounderstand więcej o nich. 
-  [Często zadawane pytania dotyczące kondycji zasobów platformy Azure](resource-health-faq.md)
- Konfigurowanie alertów, więc użytkownik jest powiadamiany o kondycji problemy. Aby uzyskać więcej informacji, zobacz [skonfigurować alerty dotyczące kondycji usługi](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md). 