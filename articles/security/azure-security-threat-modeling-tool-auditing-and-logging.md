---
title: "aaaAuditing i rejestrowania — narzędzie modelowania zagrożeń Microsoft - Azure | Dokumentacja firmy Microsoft"
description: "środki zaradcze w przypadku zagrożeń w hello narzędzie modelowania zagrożeń"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f28988833eba251b6ceb8bbd47cde37e871af609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-auditing-and-logging--mitigations"></a>Ramka zabezpieczeń: Inspekcji i rejestrowania | Środki zaradcze 
| Produktów i usług | Artykuł |
| --------------- | ------- |
| **Dynamics CRM**    | <ul><li>[Identyfikowania poufnych jednostek w rozwiązaniu i implementować inspekcji zmian](#sensitive-entities)</li></ul> |
| **Aplikacja sieci Web** | <ul><li>[Upewnij się, czy przeprowadzania inspekcji i rejestrowania są wymuszane na powitania aplikacji](#auditing)</li><li>[Upewnij się, że rotacji dziennika i oddzielenie zostały spełnione](#log-rotation)</li><li>[Upewnij się, że aplikacji hello nie rejestruje danych poufnych użytkownika](#log-sensitive-data)</li><li>[Upewnij się, że inspekcja i pliki dziennika mają dostęp ograniczony](#log-restricted-access)</li><li>[Upewnij się, że użytkownik administracyjny zdarzenia są rejestrowane](#user-management)</li><li>[Upewnij się, że hello system ma wbudowane zabezpieczenia przed niewłaściwym użyciem](#inbuilt-defenses)</li><li>[Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze aplikacji Azure](#diagnostics-logging)</li></ul> |
| **Baza danych** | <ul><li>[Upewnij się, że inspekcja logowania jest włączona na serwerze SQL](#identify-sensitive-entities)</li><li>[Włączyć wykrywanie zagrożeń SQL Azure](#threat-detection)</li></ul> |
| **Azure Storage** | <ul><li>[Użyj dostępu tooaudit analityka magazynu Azure usługi Azure Storage](#analytics)</li></ul> |
| **WCF** | <ul><li>[Implementowanie wystarczające rejestrowania](#sufficient-logging)</li><li>[Implementowanie obsługi wystarczające Niepowodzenie inspekcji](#audit-failure-handling)</li></ul> |
| **Interfejs API sieci Web** | <ul><li>[Upewnij się, że inspekcji i rejestrowania są wymuszane na interfejs API sieci Web](#logging-web-api)</li></ul> |
| **Pole IoT bramy** | <ul><li>[Upewnij się, czy odpowiedniej inspekcji i rejestrowania są wymuszane na pole bramy](#logging-field-gateway)</li></ul> |
| **Brama chmury IoT** | <ul><li>[Upewnij się, czy odpowiednie inspekcji i rejestrowania są wymuszane na bramy chmury](#logging-cloud-gateway)</li></ul> |

## <a id="sensitive-entities"></a>Identyfikowania poufnych jednostek w rozwiązaniu i implementować inspekcji zmian

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Dynamics CRM | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki**                   | Identyfikowanie jednostek w rozwiązaniu zawierające dane poufne i implementować inspekcji zmian w tych jednostek i pól |

## <a id="auditing"></a>Upewnij się, czy przeprowadzania inspekcji i rejestrowania są wymuszane na powitania aplikacji

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki**                   | Włączanie inspekcji i rejestrowania dla wszystkich składników. Dzienniki inspekcji należy przechwytywać kontekstu użytkownika. Zidentyfikuj wszystkie zdarzenia ważne i dziennika zdarzeń. Implementowanie funkcji centralnego rejestrowania |

## <a id="log-rotation"></a>Upewnij się, że rotacji dziennika i oddzielenie zostały spełnione

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki**                   | <p>Rotacji dziennika jest używany w administracji systemu, w którym są archiwizowane pliki dziennika z zautomatyzowany proces. Serwery, które często uruchamiać aplikacje dużych rejestrować wszystkie żądania: jest w fazie hello dzienników przestrzennych, rotacji dziennika jest hello toolimit sposób całkowity rozmiar dzienników hello umożliwiając analizy ostatnie zdarzenia. </p><p>Rozdzielenie dziennika zasadniczo oznacza, że toostore plików dziennika na innej partycji jako gdzie systemu operacyjnego/aplikacja jest uruchomiona w w kolejności tooavert typu "odmowa usługi" ataku lub hello zmiany na starszą wersję aplikacji jego wydajność</p>|

## <a id="log-sensitive-data"></a>Upewnij się, że aplikacji hello nie rejestruje danych poufnych użytkownika

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki**                   | <p>Sprawdź nie rejestruj żadnych poufnych danych lokacji tooyour przesyłania. Sprawdź, czy zamierzone rejestrowania, a także efekty uboczne spowodowane przez problemy z projektu. Przykłady danych poufnych:</p><ul><li>Poświadczenia użytkownika</li><li>Numer ubezpieczenia społecznego i inne informacje identyfikacyjne</li><li>Numer karty kredytowej lub inne informacje finansowe</li><li>Informacje o kondycji</li><li>Klucze prywatne lub innych danych, które mogą być używane toodecrypt zaszyfrowanych informacji</li><li>Systemu lub aplikacji informacje, które mogą być używane toomore skutecznie atak powitania aplikacji</li></ul>|

## <a id="log-restricted-access"></a>Upewnij się, że inspekcja i pliki dziennika mają dostęp ograniczony

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki**                   | <p>Sprawdź, czy pliki toolog praw dostępu tooensure są odpowiednio ustawione. Konta aplikacji powinny mieć dostęp tylko do zapisu i operatory i pomocy technicznej powinien mieć dostęp tylko do odczytu, zgodnie z potrzebami.</p><p>Konta administratorów są hello tylko konta, które ma pełny dostęp. Sprawdź, czy listy ACL systemu Windows w dzienniku pliki są poprawnie ograniczeniami tooensure:</p><ul><li>Konta aplikacji powinny mieć dostęp tylko do zapisu</li><li>Operatory i personel pomocy technicznej powinien mieć dostęp tylko do odczytu, w razie potrzeby</li><li>Administratorzy są hello tylko konta, które ma pełny dostęp</li></ul>|

## <a id="user-management"></a>Upewnij się, że użytkownik administracyjny zdarzenia są rejestrowane

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki**                   | <p>Upewnij się, że aplikacja hello monitoruje zdarzeń zarządzania użytkownika, takich jak nazwy logowania użytkownika udane i nieudane, resetowania haseł, zmiany hasła, zablokowania konta, rejestracja użytkownika. W ten sposób pomaga toodetect i reagowania na podejrzane zachowanie toopotentially. Umożliwia również toogather operacji danych. na przykład tootrack, kto uzyskuje dostęp do aplikacji hello</p>|

## <a id="inbuilt-defenses"></a>Upewnij się, że hello system ma wbudowane zabezpieczenia przed niewłaściwym użyciem

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki**                   | <p>Formanty powinny zostać zastosowane którego zgłosić wyjątek zabezpieczeń w razie niewłaściwego użycia aplikacji. Np. jeśli atakujący podejmie tooinject złośliwy kod, który nie pasuje do wyrażenia regularnego hello sprawdzania poprawności danych wejściowych jest już na miejscu, wyjątek zabezpieczeń może zostać wygenerowany może to przykładowy nadużycia systemu</p><p>Na przykład zalecane jest, wyjątki zabezpieczeń toohave rejestrowane i akcje wykonywane dla hello następujące problemy:</p><ul><li>Sprawdzania poprawności danych wejściowych</li><li>Naruszenia CSRF</li><li>Atak siłowy (górny limit liczby żądań na użytkownika na zasobów)</li><li>Naruszeń przekazywania pliku</li><ul>|

## <a id="diagnostics-logging"></a>Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze aplikacji Azure

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | EnvironmentType - Azure |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>Platforma Azure oferuje wbudowane narzędzia diagnostyczne tooassist z debugowaniem aplikacji usługi aplikacji sieci web. Ma również zastosowanie tooAPI aplikacji i aplikacji mobilnych. Aplikacje sieci web usługi aplikacji — Podaj funkcja diagnostyki dla rejestrowanie informacji z serwera sieci web hello i hello aplikacji sieci web.</p><p>Te logicznie podzielone na diagnostyki serwera sieci web i diagnostyki aplikacji</p>|

## <a id="identify-sensitive-entities"></a>Upewnij się, że inspekcja logowania jest włączona na serwerze SQL

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Konfigurowanie inspekcji logowania](https://msdn.microsoft.com/library/ms175850.aspx) |
| **Kroki** | <p>Inspekcja logowania serwera bazy danych musi być włączone toodetect/Potwierdź hasło odgadnięcie ataków. Koniecznie toocapture nieudane próby logowania. Przechwytywanie prób zarówno udane i nieudane logowania zapewnia dodatkowych korzyści podczas badania śledczej</p>|

## <a id="threat-detection"></a>Włączyć wykrywanie zagrożeń SQL Azure

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Usługi SQL Azure |
| **Atrybuty**              | Wersja programu SQL — wersja 12 |
| **Odwołania**              | [Rozpoczynanie pracy z wykrywanie zagrożeń bazy danych SQL](https://azure.microsoft.com/documentation/articles/sql-database-threat-detection-get-started/)|
| **Kroki** |<p>Wykrywanie zagrożeń wykrywa nietypowe działania bazy danych wskazujące toohello zagrożenia potencjalnych zabezpieczeń bazy danych. Zapewnia nową warstwę zabezpieczeń, co umożliwia klientom toodetect i odpowiadać toopotential zagrożeń w miarę ich występowania, zapewniając alerty zabezpieczeń w nietypowych działań.</p><p>Użytkownicy mogą Eksploruj hello zdarzenia podejrzane przy użyciu usługi Azure SQL Database Auditing toodetermine, jeśli są one wynikiem tooaccess próby naruszenia lub wykorzystać danych w bazie danych hello.</p><p>Wykrywanie zagrożeń umożliwia proste tooaddress potencjalne zagrożenia toohello bazy danych bez toobe potrzeby hello ekspert zabezpieczeń lub zarządzać zabezpieczeniami zaawansowanymi, monitorowanie systemów</p>|

## <a id="analytics"></a>Użyj dostępu tooaudit analityka magazynu Azure usługi Azure Storage

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Azure Storage | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy |
| **Odwołania**              | [Przy użyciu typu autoryzacji toomonitor analityka magazynu](https://azure.microsoft.com/documentation/articles/storage-security-guide/#storage-analytics) |
| **Kroki** | <p>Dla każdego konta magazynu jedna włączyć rejestrowanie tooperform analityka magazynu Azure i przechowywania danych metryki. Witaj magazynu analizy dzienników zawierają istotne informacje, takie jak metodę uwierzytelniania używaną przez osobę przy uzyskiwaniu dostępu do magazynu.</p><p>Może to być naprawdę pomocne, jeśli są ściśle ochrona toostorage dostępu. Na przykład w magazynie obiektów Blob można ustawić dla wszystkich tooprivate kontenery hello i zaimplementować hello korzystania z usługi SAS w całej aplikacji. Następnie można sprawdzić dzienniki hello regularnie toosee czy obiektów blob są dostępne przy użyciu kluczy konta magazynu hello, które mogą wskazywać naruszenia zabezpieczeń, czy obiekty BLOB hello są publiczne, ale nie powinny być one.</p>|

## <a id="sufficient-logging"></a>Implementowanie wystarczające rejestrowania

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | WCF | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | .NET framework |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [uzyskania zawartości Królestwo](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Kroki** | <p>Brak Hello dziennik inspekcji właściwe po zdarzenia zabezpieczeń mogą utrudniać śledczej działań. Windows Communication Foundation (WCF) oferuje prób uwierzytelnienia się pomyślnie lub niepowodzeniem toolog możliwości hello.</p><p>Rejestrowanie nieudanych prób uwierzytelnienia może zostać wyświetlone ostrzeżenie administratorów o potencjalnych ataków siłowych. Podobnie rejestrowanie zdarzeń pomyślnego uwierzytelnienia zapewniają dziennik inspekcji przydatne w przypadku złamania zabezpieczeń konta uprawnionego. Włączanie funkcji inspekcji zabezpieczeń usługi WCF w |

### <a name="example"></a>Przykład
Witaj poniżej przedstawiono przykładową konfigurację po włączeniu inspekcji
```
<system.serviceModel>
    <behaviors>
        <serviceBehaviors>
            <behavior name=""NewBehavior"">
                <serviceSecurityAudit auditLogLocation=""Default""
                suppressAuditFailure=""false"" 
                serviceAuthorizationAuditLevel=""SuccessAndFailure""
                messageAuthenticationAuditLevel=""SuccessAndFailure"" />
                ...
            </behavior>
        </servicebehaviors>
    </behaviors>
</system.serviceModel>
```

## <a id="audit-failure-handling"></a>Implementowanie obsługi wystarczające Niepowodzenie inspekcji

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | WCF | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | .NET framework |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [uzyskania zawartości Królestwo](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Kroki** | <p>Skonfigurowano rozwinięte rozwiązanie toogenerate wyjątek po błędzie dziennik inspekcji tooan toowrite. Jeśli skonfigurowano WCF toothrow zgłoszenie wyjątku, gdy jest dziennik inspekcji tooan toowrite, nie otrzymasz powiadomień hello program hello awarii i przeprowadzanie inspekcji zdarzeń krytycznych mogą nie być wykrywane.</p>|

### <a name="example"></a>Przykład
Witaj `<behavior/>` WCF powoduje, że element hello pliku konfiguracji usługi WCF poniżej toonot powiadamiania aplikacji hello WCF dziennik inspekcji tooan toowrite nie powiedzie się.
````
<behaviors>
    <serviceBehaviors>
        <behavior name="NewBehavior">
            <serviceSecurityAudit auditLogLocation="Application"
            suppressAuditFailure="true"
            serviceAuthorizationAuditLevel="Success"
            messageAuthenticationAuditLevel="Success" />
        </behavior>
    </serviceBehaviors>
</behaviors>
````
Skonfiguruj WCF toonotify hello program zawsze, gdy dziennik inspekcji tooan toowrite jest. Hello program powinien mieć schemat alternatywnych powiadomień w miejscu tooalert hello organizacji, czy zapisy inspekcji nie są obsługiwane. 

## <a id="logging-web-api"></a>Upewnij się, że inspekcji i rejestrowania są wymuszane na interfejs API sieci Web

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Interfejs API sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Włączanie inspekcji i rejestrowania na interfejsów API sieci Web. Dzienniki inspekcji należy przechwytywać kontekstu użytkownika. Zidentyfikuj wszystkie zdarzenia ważne i dziennika zdarzeń. Implementowanie funkcji centralnego rejestrowania |

## <a id="logging-field-gateway"></a>Upewnij się, czy odpowiedniej inspekcji i rejestrowania są wymuszane na pole bramy

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Pole IoT bramy | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>Wiele urządzeń, łącząc tooa pola bramy, upewnij się, że próby nawiązania połączenia i stanu uwierzytelniania (powodzenie lub niepowodzenie) dla poszczególnych urządzeń są rejestrowane i przechowywane na powitania pola bramy.</p><p>Ponadto w przypadku, gdy pole bramy jest obsługę hello Centrum IoT poświadczeń dla poszczególnych urządzeń, upewnij się, że inspekcja jest wykonywane, gdy te poświadczenia są pobierane. Tworzenie procesu tooperiodically przekazywania hello dzienniki tooAzure Centrum IoT i magazynowania do przechowywania długoterminowego.</p> |

## <a id="logging-cloud-gateway"></a>Upewnij się, czy odpowiednie inspekcji i rejestrowania są wymuszane na bramy chmury

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Brama chmury IoT | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Operacje Centrum tooIoT wprowadzenie monitorowania](https://azure.microsoft.com/documentation/articles/iot-hub-operations-monitoring/) |
| **Kroki** | <p>Projekt do gromadzenia i przechowywania danych inspekcji zebranych przez monitorowanie operacji centrum IoT. Włącz hello następujące kategorie monitorowania:</p><ul><li>Operacje tożsamości urządzenia</li><li>Komunikacja urządzenia do chmury</li><li>Komunikacja z chmury do urządzenia</li><li>Połączenia</li><li>Przekazywania plików</li></ul>|
