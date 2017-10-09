---
title: "aaaAuthorization — narzędzie modelowania zagrożeń Microsoft - Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 3ea7ae2b46baa8578e574e6006b98dfe172829e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-authorization--mitigations"></a>Ramka zabezpieczeń: Autoryzacji | Środki zaradcze 
| Produktów i usług | Artykuł |
| --------------- | ------- |
| **Granic zaufania maszyny** | <ul><li>[Upewnij się, że odpowiednie listy kontroli dostępu skonfigurowanych toorestrict nieautoryzowany dostęp toodata na urządzeniu hello](#acl-restricted-access)</li><li>[Upewnij się, że zawartość poufnej aplikacji specyficzne dla użytkownika jest przechowywana w katalogu profilu użytkownika](#sensitive-directory)</li><li>[Upewnij się, że hello wdrożone aplikacje są uruchamiane z najmniejszymi uprawnieniami](#deployed-privileges)</li></ul> |
| **Aplikacja sieci Web** | <ul><li>[Wymusić kolejności kolejny krok podczas przetwarzania przepływów logika biznesowa](#sequential-logic)</li><li>[Implementowanie szybkość ograniczanie mechanizm tooprevent wyliczania](#rate-enumeration)</li><li>[Sprawdź, czy odpowiednie autoryzacji jest już na miejscu i następuje reguły najniższych uprawnień](#principle-least-privilege)</li><li>[Logika i zasobów dostępu autoryzacji decyzje biznesowe nie powinny być oparte na przychodzące parametry żądania](#logic-request-parameters)</li><li>[Upewnij się, że zawartość i zasoby nie są wyliczalny ani dostępne za pośrednictwem wymuszone przeglądania](#enumerable-browsing)</li></ul> |
| **Baza danych** | <ul><li>[Upewnij się, że najmniej uprzywilejowane konta są używane tooconnect tooDatabase serwera](#privileged-server)</li><li>[Implementowanie kontrola dostępu zabezpieczeń na poziomie wiersza tooprevent dzierżawcom dostęp do siebie nawzajem danych](#rls-tenants)</li><li>[Rola administratora systemu powinien mieć tylko niezbędne użytkowników](#sysadmin-users)</li></ul> |
| **Brama chmury IoT** | <ul><li>[Połącz tooCloud bramy przy użyciu najmniej uprzywilejowane tokenów](#cloud-least-privileged)</li></ul> |
| **Centrum zdarzeń platformy Azure** | <ul><li>[Użyj uprawnień tylko do wysyłania klucza sygnatury dostępu Współdzielonego do generowania tokenów urządzenia](#sendonly-sas)</li><li>[Nie używaj tokenów dostępu, które zapewniają toohello bezpośredni dostęp do Centrum zdarzeń](#access-tokens-hub)</li><li>[Połącz tooEvent, który Centrum przy użyciu sygnatury dostępu Współdzielonego kluczy, że ma hello minimalne wymagane uprawnienia](#sas-minimum-permissions)</li></ul> |
| **Dokumentów w usłudze Azure DB** | <ul><li>[Użyj zasobu tokenów tooconnect tooDocumentDB zawsze, gdy jest to możliwe](#resource-docdb)</li></ul> |
| **Granic zaufania Azure** | <ul><li>[Włącz dostęp do szczegółowych zarządzania tooAzure subskrypcji przy użyciu funkcji RBAC](#grained-rbac)</li></ul> |
| **Granic zaufania sieci szkieletowej usług** | <ul><li>[Ograniczenia operacji toocluster dostępu klienta przy użyciu funkcji RBAC](#cluster-rbac)</li></ul> |
| **Dynamics CRM** | <ul><li>[Wykonaj modelowania zabezpieczeń i używać zabezpieczeń na poziomie pola w przypadku, gdy wymagane](#modeling-field)</li></ul> |
| **Portal programu Dynamics CRM** | <ul><li>[Wykonaj modelowania zabezpieczeń w portalu konta, pamiętając hello modelu zabezpieczeń dla portalu hello różni się od reszty hello CRM](#portal-security)</li></ul> |
| **Azure Storage** | <ul><li>[Udziel uprawnień szczegółowych zakresu jednostek w magazynie tabel platformy Azure](#permission-entities)</li><li>[Włącz konto magazynu tooAzure kontroli dostępu opartej na rolach (RBAC) przy użyciu usługi Azure Resource Manager](#rbac-azure-manager)</li></ul> |
| **Klientów urządzeń przenośnych** | <ul><li>[Implementowanie niejawne zdjęcia lub umieszczanie w katalogu głównym wykrywania](#rooting-detection)</li></ul> |
| **WCF** | <ul><li>[Odwołanie słabe klasy w programie WCF](#weak-class-wcf)</li><li>[Formant autoryzacji wdrożenie usługi WCF](#wcf-authz)</li></ul> |
| **Interfejs API sieci Web** | <ul><li>[Implementuje mechanizm właściwą autoryzację w interfejsie API sieci Web ASP.NET](#authz-aspnet)</li></ul> |
| **Urządzenia IoT** | <ul><li>[Wykonaj sprawdzanie autoryzacji w hello urządzenia, jeśli obsługuje różne akcje, które wymagają różne poziomy uprawnień](#device-permission)</li></ul> |
| **Pole IoT bramy** | <ul><li>[Wykonaj sprawdzanie autoryzacji w hello pola bramy, jeśli obsługuje różne akcje, które wymagają różne poziomy uprawnień](#field-permission)</li></ul> |

## <a id="acl-restricted-access"></a>Upewnij się, że odpowiednie listy kontroli dostępu skonfigurowanych toorestrict nieautoryzowany dostęp toodata na urządzeniu hello

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Granic zaufania maszyny | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Upewnij się, że odpowiednie listy kontroli dostępu skonfigurowanych toorestrict nieautoryzowany dostęp toodata na urządzeniu hello|

## <a id="sensitive-directory"></a>Upewnij się, że zawartość poufnej aplikacji specyficzne dla użytkownika jest przechowywana w katalogu profilu użytkownika

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Granic zaufania maszyny | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Upewnij się, że zawartość poufnej aplikacji specyficzne dla użytkownika jest przechowywana w katalogu profilu użytkownika. Jest to tooprevent wielu użytkowników hello komputera uzyskanie dostępu do danych siebie nawzajem.|

## <a id="deployed-privileges"></a>Upewnij się, że hello wdrożone aplikacje są uruchamiane z najmniejszymi uprawnieniami

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Granic zaufania maszyny | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Upewnij się, że aplikacja hello wdrożone jest uruchamiana z najmniejszymi uprawnieniami. |

## <a id="sequential-logic"></a>Wymusić kolejności kolejny krok podczas przetwarzania przepływów logika biznesowa

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | W kolejności tooverify uruchomionego za pomocą tego etapu przez użytkownika oryginalny tooenforce hello aplikacji tooonly firm logiki przepływy procesu w kolejności kolejny krok wszystkich kroków przetwarzanych w czasie człowieka realistyczne, a następnie przetwarza poza kolejnością, pominięte kroki, przetwarzane kroki od innego użytkownika lub zbyt szybko przesłać transakcji.|

## <a id="rate-enumeration"></a>Implementowanie szybkość ograniczanie mechanizm tooprevent wyliczania

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Upewnij się, czy losowe identyfikatory poufnych. Wdrażanie kontroli CAPTCHA na stronach anonimowy. Upewnij się, że błędów i wyjątków nie powinny ujawniać określonych danych|

## <a id="principle-least-privilege"></a>Sprawdź, czy odpowiednie autoryzacji jest już na miejscu i następuje reguły najniższych uprawnień

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>zasada Hello oznacza, podając konto użytkownika, tylko te uprawnienia, które są niezbędne toothat pracy użytkowników. Na przykład kopii zapasowych użytkownik nie musi oprogramowania tooinstall: w związku z tym hello kopii zapasowej użytkownika ma prawa toorun tylko tworzenia kopii zapasowej i związanych z kopii zapasowej aplikacji. Inne uprawnienia, takie jak instalowanie nowego oprogramowania są zablokowane. Witaj zasada ma zastosowanie również tooa komputerów osobistych użytkownika, który zwykle działa w normalne konto użytkownika i otwiera konta uprzywilejowanego, chroniony hasłem (superuser) tylko, gdy okoliczności hello wymaga go całkowicie. </p><p>Ta zasada może być również aplikacji sieci web tooyour zastosowane. Zamiast wyłącznie w zależności od metody uwierzytelniania opartej na rolach przy użyciu sesji, a nie chcemy się, że tooassign uprawnienia toousers za pomocą uwierzytelniania na podstawie bazy danych systemu. Firma Microsoft Jeśli nadal używać sesji w kolejności tooidentify hello był zalogowany użytkownik prawidłowo, tylko teraz zamiast przypisywać tooperform uprzywilejowanego w systemie hello tego użytkownika z możemy przypisać mu z uprawnieniami tooverify akcje, które ma określoną rolę. Duży pro tej metody jest także, gdy użytkownik ma przypisane uprawnienia mniej, zmiany zostaną zastosowane na bieżąco hello, ponieważ przypisanie hello nie zależy od hello sesji, które w przeciwnym razie ma tooexpire najpierw toobe.</p>|

## <a id="logic-request-parameters"></a>Logika i zasobów dostępu autoryzacji decyzje biznesowe nie powinny być oparte na przychodzące parametry żądania

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Zawsze, gdy są sprawdzanie, czy użytkownik jest ograniczony tooreview niektórych danych access hello ograniczenia powinny być przetwarzane po stronie serwera. Identyfikator użytkownika Hello powinny być przechowywane w zmiennej sesji podczas logowania i powinna być używana tooretrieve użytkownika dane z bazy danych hello |

### <a name="example"></a>Przykład
```SQL
SELECT data 
FROM personaldata 
WHERE userID=:id < - session var 
```
Teraz nie atakujący możliwe modyfikację i zmienić hello operacji aplikacji, ponieważ hello identyfikator pobierania powitalne danych jest obsługiwane po stronie serwera.

## <a id="enumerable-browsing"></a>Upewnij się, że zawartość i zasoby nie są wyliczalny ani dostępne za pośrednictwem wymuszone przeglądania

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>Poufne pliki statyczne i konfiguracji nie powinny być przechowywane w hello katalogiem głównym sieci web. Dla zawartości publicznej toobe nie jest wymagane właściwy dostęp, które można zastosować kontroli lub usuwania hello zawartości samej siebie.</p><p>Ponadto przeglądanie wymuszone zwykle w połączeniu z siłowych techniki toogather informacji przez podejmowanie próby tooaccess dowolną liczbę adresów URL jako możliwych tooenumerate katalogów i plików na serwerze. Osoby atakujące mogą sprawdzić wszystkie odmiany często istniejących plików. Na przykład wyszukiwania plików hasła może obejmować pliki w tym psswd.txt, password.htm password.dat i innych zmian.</p><p>toomitigate to możliwości wykrywania siłowych prób mają zostać uwzględnione.</p>|

## <a id="privileged-server"></a>Upewnij się, że najmniej uprzywilejowane konta są używane tooconnect tooDatabase serwera

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Baza danych SQL uprawnienia hierarchii](https://msdn.microsoft.com/library/ms191465), [zabezpieczanych obiektów bazy danych SQL](https://msdn.microsoft.com/library/ms190401) |
| **Kroki** | Najmniej uprzywilejowane konta powinna być używana tooconnect toohello w bazie danych. Logowania aplikacji powinny być ograniczone w bazie danych hello i mają być wykonywane tylko wybrane procedury składowane. Logowania aplikacji powinien mieć nie bezpośredniego dostępu do tabel. |

## <a id="rls-tenants"></a>Implementowanie kontrola dostępu zabezpieczeń na poziomie wiersza tooprevent dzierżawcom dostęp do siebie nawzajem danych

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Lokalnego programu SQL Azure |
| **Atrybuty**              | MsSQL2016 wersji — w wersji 12, wersja programu SQL — SQL |
| **Odwołania**              | [Zabezpieczenia na poziomie wiersza serwera SQL (kontrola dostępu)](https://msdn.microsoft.com/library/azure/dn765131.aspx) |
| **Kroki** | <p>Zabezpieczenia na poziomie wiersza umożliwia klientom toocontrol dostępu toorows w tabeli bazy danych na podstawie charakterystyk hello użytkownika hello wykonywania zapytania (np. grupy członkostwa lub wykonywania context).</p><p>Wiersz poziom zabezpieczeń kontrola dostępu ułatwia hello projektu i kodowania zabezpieczeń w aplikacji. Kontrola dostępu umożliwia tooimplement ograniczenia dostępu do wiersza danych. Na przykład zapewnienie, że pracownicy mogą uzyskiwać dostęp do tylko te wiersze danych, które są odpowiednie tootheir działu lub ograniczanie dostępu do danych klienta tooonly firmy tootheir odpowiednich danych hello.</p><p>Logika ograniczenie dostępu Hello jest znajduje się w hello warstwy bazy danych zamiast od hello danych w innej warstwie aplikacji. Witaj bazy danych systemu stosuje ograniczenia dostępu hello za każdym razem, gdy nastąpiła by dostęp do danych z dowolnej wersji. W efekcie hello zabezpieczeń systemu bardziej niezawodne i niezawodne zmniejszając hello powierzchni hello zabezpieczeń systemu.</p><p>|

Należy pamiętać, że zabezpieczenia na poziomie wiersza jako funkcja poza pole bazy danych jest zastosowanie tooSQL tylko od 2016 serwera i bazy danych Azure SQL. Jeśli hello poza pole zabezpieczenia na poziomie wiersza funkcja nie jest zaimplementowana, należy zapewnić, że dostęp do danych jest ograniczony przy użyciu widoków i procedur

## <a id="sysadmin-users"></a>Rola administratora systemu powinien mieć tylko niezbędne użytkowników

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Baza danych SQL uprawnienia hierarchii](https://msdn.microsoft.com/library/ms191465), [zabezpieczanych obiektów bazy danych SQL](https://msdn.microsoft.com/library/ms190401) |
| **Kroki** | Członkowie stałej roli serwera SysAdmin hello powinny być bardzo ograniczoną i nigdy nie zawiera konta używane przez aplikacje.  Przejrzyj listę użytkowników w roli hello hello i usunąć wszystkie zbędne konta|

## <a id="cloud-least-privileged"></a>Połącz tooCloud bramy przy użyciu najmniej uprzywilejowane tokenów

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Brama chmury IoT | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Wybór bramy - Centrum IoT Azure |
| **Odwołania**              | [Kontrolę dostępu Centrum iot](https://azure.microsoft.com/documentation/articles/iot-hub-devguide/#Security) |
| **Kroki** | Podaj najniższych uprawnień składników toovarious uprawnienia, które połączyć tooCloud bramy (Centrum IoT). Typowym przykładem jest — składnika zainicjowania/zarządzania urządzeniami używa registryread/zapisu, zdarzenie procesora (ASA) korzysta z połączenia usługi. Poszczególne urządzenia łączyć się przy użyciu poświadczeń urządzenia|

## <a id="sendonly-sas"></a>Użyj uprawnień tylko do wysyłania klucza sygnatury dostępu Współdzielonego do generowania tokenów urządzenia

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Centrum zdarzeń platformy Azure | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Uwierzytelnianie i zabezpieczenia modelu Omówienie usługi Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Kroki** | Klucz sygnatury dostępu Współdzielonego jest używane toogenerate tokenów poszczególnych urządzeń. Użycia klucza sygnatury dostępu Współdzielonego uprawnienia tylko do wysyłania podczas generowania tokenu urządzenia powitania dla danego wydawcy|

## <a id="access-tokens-hub"></a>Nie używaj tokenów dostępu, które zapewniają toohello bezpośredni dostęp do Centrum zdarzeń

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Centrum zdarzeń platformy Azure | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Uwierzytelnianie i zabezpieczenia modelu Omówienie usługi Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Kroki** | Token, który przyznaje Centrum zdarzeń toohello bezpośredni dostęp nie powinny być podawane toohello urządzenia. Za pomocą tokenu najniższych uprawnieniach urządzenia hello, zapewniająca dostęp, który tylko tooa wydawcy może pomóc w identyfikacji i wyeliminować go, jeśli znaleziono toobe nieautoryzowanego lub naruszony urządzenia.|

## <a id="sas-minimum-permissions"></a>Połącz tooEvent, który Centrum przy użyciu sygnatury dostępu Współdzielonego kluczy, że ma hello minimalne wymagane uprawnienia

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Centrum zdarzeń platformy Azure | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Uwierzytelnianie i zabezpieczenia modelu Omówienie usługi Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Kroki** | Podaj co najmniej uprawnień uprawnienia toovarious zaplecza aplikacji łączących toohello Centrum zdarzeń. Generowanie oddzielnych klucza sygnatury dostępu Współdzielonego dla każdej aplikacji zaplecza i tylko hello wymagane uprawnienia - toothem wysyłania i odbierania zarządzanie.|

## <a id="resource-docdb"></a>Użyj zasobu tokenów tooconnect tooCosmos bazy danych, jeśli to możliwe

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Dokumentów w usłudze Azure DB | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Token zasobu jest skojarzony z zasobem uprawnienia usługi DocumentDB i przechwytywania hello relacji między hello użytkownika bazy danych i hello uprawnienia, które użytkownik ma dla określonego zasobu aplikacji usługi DocumentDB (np. kolekcji i dokumentów). Jeśli powitania klienta nie jest zaufany z postępowania z kluczami głównego lub w trybie tylko do odczytu — podobnie jak klient przenośnego lub stacjonarnego aplikacji użytkownika należy zawsze używać hello tokenu tooaccess zasobów usługi DocumentDB. Użyj klucza głównego lub tylko do odczytu klucze z wewnętrznej bazy danych aplikacji, które można bezpiecznie przechowywać klucze.|

## <a id="grained-rbac"></a>Włącz dostęp do szczegółowych zarządzania tooAzure subskrypcji przy użyciu funkcji RBAC

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Granic zaufania Azure | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Użyj roli przypisania toomanage dostępu tooyour subskrypcji platformy Azure zasobów](https://azure.microsoft.com/documentation/articles/role-based-access-control-configure/)  |
| **Kroki** | Kontrola dostępu oparta na rolach (Role-Based Access Control, RBAC) na platformie Azure umożliwia precyzyjne zarządzanie dostępem dla platformy Azure. Przy użyciu funkcji RBAC, można udzielić tylko hello takiego dostępu czy użytkownicy muszą tooperform swoich zadań.|

## <a id="cluster-rbac"></a>Ograniczenia operacji toocluster dostępu klienta przy użyciu funkcji RBAC

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Granic zaufania sieci szkieletowej usług | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Środowisko — Azure |
| **Odwołania**              | [Kontrola dostępu oparta na rolach dla klientów sieci szkieletowej usług](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security-roles/) |
| **Kroki** | <p>Sieć szkieletowa usług Azure obsługuje dwa typy kontroli różny dostęp dla klientów, które są połączone tooa klastra sieci szkieletowej usług: administratora i użytkownika. Kontrola dostępu umożliwia hello klastra administrator toolimit dostępu toocertain klastra operacje dla różnych grup użytkowników, co klaster hello bardziej bezpieczne.</p><p>Administratorzy mają pełny dostęp toomanagement możliwości (w tym możliwości odczytu/zapisu). Użytkownicy mają domyślnie tylko możliwości toomanagement dostęp do odczytu (na przykład możliwość wykonywania kwerend), a hello możliwości tooresolve aplikacji i usług.</p><p>Witaj dwie role klient (administratora i klient) określa się w czasie hello tworzenia klastra, podając oddzielne certyfikaty dla każdego.</p>|

## <a id="modeling-field"></a>Wykonaj modelowania zabezpieczeń i używać zabezpieczeń na poziomie pola w przypadku, gdy wymagane

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Dynamics CRM | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Wykonaj modelowania zabezpieczeń i używać zabezpieczeń na poziomie pola w przypadku, gdy wymagane|

## <a id="portal-security"></a>Wykonaj modelowania zabezpieczeń w portalu konta, pamiętając hello modelu zabezpieczeń dla portalu hello różni się od reszty hello CRM

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Portal programu Dynamics CRM | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Wykonaj modelowania zabezpieczeń w portalu konta, pamiętając hello modelu zabezpieczeń dla portalu hello różni się od reszty hello CRM|

## <a id="permission-entities"></a>Udziel uprawnień szczegółowych zakresu jednostek w magazynie tabel platformy Azure

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Azure Storage | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | StorageType - tabeli |
| **Odwołania**              | [Jak toodelegate dostępu tooobjects na koncie magazynu platformy Azure przy użyciu sygnatury dostępu Współdzielonego](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_data-plane-security) |
| **Kroki** | W niektórych scenariuszy biznesowych magazynu tabel Azure może być wymagane toostore dane poufne, które może toodifferent strony. Np. poufnych danych dotyczących toodifferent krajach. W takich przypadkach sygnatury SAS można konstruować określając hello partycji i wiersza zakresami kluczy, tak, aby użytkownik mógł korzystać z danego kraju tooa określonych danych.| 

## <a id="rbac-azure-manager"></a>Włącz konto magazynu tooAzure kontroli dostępu opartej na rolach (RBAC) przy użyciu usługi Azure Resource Manager

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Azure Storage | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Jak toosecure, konto magazynu, z kontroli dostępu opartej na rolach (RBAC)](https://azure.microsoft.com/documentation/articles/storage-security-guide/#management-plane-security) |
| **Kroki** | <p>Podczas tworzenia nowego konta magazynu jest wybierz model wdrożenia klasycznego lub usługi Azure Resource Manager. Witaj klasycznego modelu tworzenie zasobów na platformie Azure tylko umożliwia subskrypcji toohello all-or-nothing dostępu i z kolei hello konta magazynu.</p><p>Model usługi Azure Resource Manager hello możesz zaznaczyć hello konta magazynu zasobów grupy i kontroli dostępu toohello zarządzania płaszczyźnie tego konta określonego magazynu przy użyciu usługi Azure Active Directory. Na przykład możesz zapewnić określonych użytkowników hello możliwości tooaccess hello klucze konta magazynu, podczas gdy inni użytkownicy mogą wyświetlać informacje o koncie magazynu hello, ale nie ma dostępu do kluczy konta magazynu hello.</p>|

## <a id="rooting-detection"></a>Implementowanie niejawne zdjęcia lub umieszczanie w katalogu głównym wykrywania

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Klientów urządzeń przenośnych | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>Aplikacja powinna chronić własnych danych konfiguracji i użytkownika w przypadku, jeśli telefon jest ścieżką do katalogu głównego lub ma zdjęte zabezpieczenia systemu. Umieszczanie katalogu głównym/zdjęto zabezpieczeń fundamentalne oznacza nieautoryzowanym dostępem, normalnych użytkowników, którzy nie są na ich własnych telefonów. W związku z tym aplikacji powinien mieć logikę wykrywania niejawne podczas uruchamiania aplikacji, toodetect Jeśli odblokowany dostęp hello telefonu.</p><p>Logika wykrywania Hello można po prostu uzyskiwać dostęp do plików, które zwykle tylko główny użytkownik może uzyskać dostęp, na przykład:</p><ul><li>/System/App/SUPERUSER.apk</li><li>/ sbin/su</li><li>/System/bin/su</li><li>/System/xbin/su</li><li>/Data/Local/xbin/su</li><li>/Data/local/bin/su</li><li>/System/SD/xbin/su</li><li>/System/bin/FailSafe/su</li><li>/Data/Local/su</li></ul><p>Aplikacji hello można uzyskać dostępu do żadnego z tych plików, oznacza, że aplikacja hello jest uruchomiona jako użytkownik root.</p>|

## <a id="weak-class-wcf"></a>Odwołanie słabe klasy w programie WCF

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | WCF | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny, NET Framework 3 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [uzyskania zawartości Królestwo](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Kroki** | <p>Witaj system używa Odwołanie słabe klasy, które osoba atakująca może mieć tooexecute nieautoryzowanego kodu. Hello program odwołuje się do klasy zdefiniowanej przez użytkownika, która nie jest jednoznacznie zidentyfikować. Załadowanie tej klasy lekko zidentyfikowanych hello CLR typu modułu ładującego wyszukuje klasy hello w następującej lokalizacji w hello hello .NET określić kolejność:</p><ol><li>Jeśli zestawu hello typu hello jest znany, wyszukiwanie modułu ładującego hello hello pliku konfiguracji przekierowania lokalizacji pamięci podręcznej GAC, hello bieżącego zestawu za pomocą informacji o konfiguracji i hello podstawowego katalogu aplikacji</li><li>Jeśli zestaw hello jest nieznany, wyszukiwanie modułu ładującego hello hello bieżącego zestawu, mscorlib i lokalizację hello zwrócony przez program obsługi zdarzeń TypeResolve hello</li><li>Ta kolejność wyszukiwania CLR można modyfikować punkty zaczepienia, takich jak hello mechanizm przekazywania typu i hello AppDomain.TypeResolve zdarzeń</li></ol><p>Jeśli osoba atakująca wykorzystuje kolejność wyszukiwania CLR hello tworząc hello alternatywnych klasy z samą nazwę i umieszczenie go w lokalizacji alternatywnej tego powitalne CLR załaduje najpierw, hello CLR przypadkowo wykona hello dostarczone przez osobę atakującą kodu</p>|

### <a name="example"></a>Przykład
Witaj `<behaviorExtensions/>` element hello pliku konfiguracji usługi WCF poniżej nakazuje tooadd WCF zachowanie niestandardowej klasy tooa określonego rozszerzenia programu WCF.
```
<system.serviceModel>
    <extensions>
        <behaviorExtensions>
            <add name=""myBehavior"" type=""MyBehavior"" />
        </behaviorExtensions>
    </extensions>
</system.serviceModel>
```
Przy użyciu w pełni kwalifikowane nazwy (silne) unikatowo identyfikuje typ i jeszcze bardziej podkreśla zabezpieczenia systemu. Podczas rejestrowania typów w pliku machine.config i app.config hello w pliku, należy użyć zestawu w pełni kwalifikowanej nazwy.

### <a name="example"></a>Przykład
Witaj `<behaviorExtensions/>` WCF tooadd silnie odwołanie do zachowania niestandardowego klasy tooa określonego rozszerzenia WCF powoduje, że element hello pliku konfiguracji usługi WCF poniżej.
```
<system.serviceModel>
    <extensions>
        <behaviorExtensions>
            <add name=""myBehavior"" type=""Microsoft.ServiceModel.Samples.MyBehaviorSection, MyBehavior,
            Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"" />
        </behaviorExtensions>
    </extensions>
</system.serviceModel>
```

## <a id="wcf-authz"></a>Formant autoryzacji wdrożenie usługi WCF

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | WCF | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny, NET Framework 3 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [uzyskania zawartości Królestwo](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Kroki** | <p>Ta usługa korzysta z kontrolki autoryzacji. Kiedy klient wywołuje określonej usługi WCF, WCF zawiera różnych systemów autoryzacji, które pozwalają sprawdzić, czy ten obiekt wywołujący hello ma metody usługi hello tooexecute uprawnień na powitania serwera. Jeśli formanty autoryzacji nie są włączone dla usługi WCF, uwierzytelniony użytkownik może osiągnąć podwyższenie poziomu uprawnień.</p>|

### <a name="example"></a>Przykład
powitania po konfiguracji powoduje, że poziom autoryzacji WCF toonot wyboru hello powitania klienta podczas wykonywania hello usługi:
```
<behaviors>
    <serviceBehaviors>
        <behavior>
            ...
            <serviceAuthorization principalPermissionMode=""None"" />
        </behavior>
    </serviceBehaviors>
</behaviors>
```
Użyj usługi tooverify schemat autoryzacji, które hello wywołujący metody usługi hello jest autoryzowanym toodo tak. Usługi WCF dostępne są dwa tryby i pozwala na określenie hello schematu niestandardowej autoryzacji. Tryb UseWindowsGroups Hello korzysta role systemu Windows i użytkowników, a tryb UseAspNetRoles hello dostawcy ról ASP.NET, takich jak SQL Server, tooauthenticate.

### <a name="example"></a>Przykład
Witaj następująca konfiguracja powoduje, że WCF toomake się, że klient hello jest częścią grupy Administratorzy hello przed wykonaniem hello Dodaj usługi:
```
<behaviors>
    <serviceBehaviors>
        <behavior>
            ...
            <serviceAuthorization principalPermissionMode=""UseWindowsGroups"" />
        </behavior>
    </serviceBehaviors>
</behaviors>
```
Usługa Hello następnie jest zadeklarowany jako hello następujące czynności:
```
[PrincipalPermission(SecurityAction.Demand,
Role = ""Builtin\\Administrators"")]
public double Add(double n1, double n2)
{
double result = n1 + n2;
return result;
}
```

## <a id="authz-aspnet"></a>Implementuje mechanizm właściwą autoryzację w interfejsie API sieci Web ASP.NET

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Interfejs API sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny, MVC5 |
| **Atrybuty**              | Brak dostawcy tożsamości dostawca — usługi AD FS, tożsamość — usługi Azure AD |
| **Odwołania**              | [Uwierzytelnianie i autoryzacja w składniku ASP.NET Web API](http://www.asp.net/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api) |
| **Kroki** | <p>Informacje o rolach dla użytkowników aplikacji hello mogą być uzyskane z usługi Azure AD lub oświadczenia usług AD FS, jeśli aplikacja hello opiera się na nich jako dostawca tożsamości lub może sama aplikacja hello pod warunkiem, że. W żadnym z tych przypadkach hello autoryzacji niestandardowej implementacji należy zweryfikować informacje o rolach użytkownika hello.</p><p>Informacje o rolach dla użytkowników aplikacji hello mogą być uzyskane z usługi Azure AD lub oświadczenia usług AD FS, jeśli aplikacja hello opiera się na nich jako dostawca tożsamości lub może sama aplikacja hello pod warunkiem, że. W żadnym z tych przypadkach hello autoryzacji niestandardowej implementacji należy zweryfikować informacje o rolach użytkownika hello.</p>

### <a name="example"></a>Przykład
```C#
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
public class ApiAuthorizeAttribute : System.Web.Http.AuthorizeAttribute
{
        public async override Task OnAuthorizationAsync(HttpActionContext actionContext, CancellationToken cancellationToken)
        {
            if (actionContext == null)
            {
                throw new Exception();
            }

            if (!string.IsNullOrEmpty(base.Roles))
            {
                bool isAuthorized = ValidateRoles(actionContext);
                if (!isAuthorized)
                {
                    HandleUnauthorizedRequest(actionContext);
                }
            }

            base.OnAuthorization(actionContext);
        }

public bool ValidateRoles(actionContext)
{
   //Authorization logic here; returns true or false
}

}
```
Witaj wszystkich kontrolerów i metod akcji, których potrzebuje tooprotected powinien ozdobione powyżej atrybutu.
```C#
[ApiAuthorize]
public class CustomController : ApiController
{
     //Application code goes here
}
```

## <a id="device-permission"></a>Wykonaj sprawdzanie autoryzacji w hello urządzenia, jeśli obsługuje różne akcje, które wymagają różne poziomy uprawnień

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Urządzenia IoT | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>Hello urządzenia należy zezwolić toocheck wywołującego hello, jeśli hello wywołującego ma żądanej hello wymagane uprawnienia tooperform hello akcji. Np. umożliwia powiedz urządzenia hello jest blokady inteligentnej drzwi, które można monitorować z hello chmury, a także udostępnia funkcje, takie jak zdalne Blokowanie drzwi hello.</p><p>Hello blokady inteligentnej drzwi udostępnia funkcje odblokowywaniem tylko wtedy, gdy ktoś fizycznie jest niemal drzwi hello przy użyciu karty. W takim przypadku hello implementacja polecenia zdalnego hello i formantu ma się odbywać w taki sposób, że nie oferuje drzwi hello toounlock funkcji jako brama chmury hello nie jest autoryzowany toosend drzwi hello toounlock polecenia.</p>|

## <a id="field-permission"></a>Wykonaj sprawdzanie autoryzacji w hello pola bramy, jeśli obsługuje różne akcje, które wymagają różne poziomy uprawnień

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Pole IoT bramy | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Hello pola bramy należy zezwolić toocheck wywołującego hello Jeśli hello wywołującego ma żądanej hello wymagane uprawnienia tooperform hello akcji. Np. powinna być różne uprawnienia dla użytkownika administratora interfejsu/API używanych tooconfigure urządzeń v/s bramy pola, łączących tooit.|
