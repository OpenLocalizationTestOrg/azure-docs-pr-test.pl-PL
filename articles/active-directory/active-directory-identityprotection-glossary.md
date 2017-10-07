---
title: "aaaAzure słownik ochrony tożsamości w usłudze Active Directory | Dokumentacja firmy Microsoft"
description: "Słownik ochrony tożsamości usługi Azure Active Directory"
services: active-directory
keywords: "ochronę tożsamości usługi Azure active directory, usługa cloud app discovery, zarządzanie aplikacjami, zabezpieczeń, ryzyka, poziom ryzyka, luki w zabezpieczeniach, zasady zabezpieczeń, słownik"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 833119a5-33d6-4482-adda-fa35218c72c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ff2e96d20e2a3f1df24b78e66be5a0c6807e60a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-glossary"></a>Słownik ochrony tożsamości usługi Azure Active Directory
### <a name="at-risk-user"></a>Zagrożone (użytkownika)
Użytkownik z jednego lub wielu zdarzeń active ryzyka. 

### <a name="atypical-sign-in-location"></a>Nietypowe logowania w lokalizacji
Logowania z lokalizacji geograficznej, które nie są typowe dla określonego użytkownika hello, podobne użytkowników lub hello dzierżawy.

### <a name="azure-ad-identity-protection"></a>Usługa Azure AD Identity Protection
Moduł zabezpieczeń usługi Azure Active Directory, która udostępnia skonsolidowany wgląd w zdarzenia o podwyższonym ryzyku i potencjalnych luk w zabezpieczeniach wpływających na tożsamości organizacji.

### <a name="conditional-access"></a>Dostęp warunkowy
Zasady dotyczące zabezpieczania tooresources dostępu. Zasady dostępu warunkowego są przechowywane w hello Azure Active Directory i są oceniane przez usługę Azure AD przed udzieleniem im dostępu do zasobów toohello.  Przykład reguły obejmują, ograniczanie dostępu na podstawie lokalizacji użytkownika metodę uwierzytelniania użytkownika lub kondycji urządzenia.

### <a name="credentials"></a>Poświadczenia
Informacje, która zawiera identyfikator i potwierdzenie identyfikatora, który jest używany toogain dostępu toolocal i zasobów sieciowych. Przykładami poświadczeń są nazwy użytkownika i hasła, karty inteligentne i certyfikaty.

### <a name="event"></a>Wydarzenie
Rekord działania w usłudze Azure Active Directory.

### <a name="false-positive-risk-event"></a>Fałszywie dodatnich (ryzyka zdarzenie)
Stan zdarzenia ryzyka ustawionych ręcznie przez użytkownika ochronę tożsamości, wskazującą zdarzenie ryzyka hello została zbadana i został niepoprawnie oznaczone jako zdarzenie ryzyka.

### <a name="identity"></a>Tożsamość
Osoba lub podmiot, należy sprawdzić za pomocą uwierzytelniania na podstawie kryteriów, takie jak hasła lub certyfikatu.

### <a name="identity-risk-event"></a>Zdarzenie ryzyka tożsamości
Zdarzenie usługi AAD został oznaczony jako nietypowych przez ochronę tożsamości, która może wskazywać, że naruszono tożsamości.

### <a name="ignored-risk-event"></a>Ignorowane (ryzyka zdarzenie)
Stan zdarzenia ryzyka ustawionych ręcznie przez użytkownika ochronę tożsamości, wskazujący, że zdarzenie ryzyka hello jest zamknięty bez podejmowania działań korygujących.

### <a name="impossible-travel-from-atypical-locations"></a>Niemożliwa podróż z nietypowych lokalizacji
To zdarzenie ryzyka wyzwalane, gdy dwa logowania dla hello tego samego użytkownika zostaną wykryte, gdy co najmniej jeden z nich jest z nietypowych lokalizacji logowania, a w przypadku, gdy hello czas między logowania hello jest krótszy niż minimalny hello czasu zajmie toophysically przesyłane między tymi lokalizacje.  

### <a name="investigation"></a>Badanie
Witaj proces oceny hello działań, dzienniki i inne istotne informacje związane z tooa ryzyka zdarzeń toodecide czy korygowania lub migracji kroki są niezbędne, zrozumieć czy i jak tożsamość hello zostało naruszone i wiedzieć, jak hello. użyto tożsamości ze złamanymi zabezpieczeniami.

### <a name="leaked-credentials"></a>Ujawnione poświadczenia
To zdarzenie ryzyka wyzwalane, gdy znajdują się bieżące poświadczenia użytkownika (nazwy użytkownika i hasło) publikowane publicznie hello ciemny sieci web przez naszych pracowników naukowo-badawczych.

### <a name="mitigation"></a>Środki zaradcze
Toolimit akcji lub wyeliminowanie możliwości hello tooexploit atakująca złamany tożsamości lub urządzenia bez przywracania hello tożsamości lub urządzenie tooa bezpieczne. Środki zaradcze nie można rozpoznać poprzednie zdarzenia ryzyko związane z tożsamości hello lub urządzenia.

### <a name="multi-factor-authentication"></a>Uwierzytelnianie wieloskładnikowe
Metoda uwierzytelniania, która wymaga dwóch lub więcej metod uwierzytelniania, które mogą obejmować coś, co użytkownik hello ma taki certyfikat; coś zna hello użytkownika, takie jak nazwy użytkowników, hasła lub wyrażenia przebiegu; Atrybuty fizyczne, takie jak odcisk palca; i atrybuty osobistych, takich jak osobiste podpisu.

### <a name="offline-detection"></a>Wykrywanie w trybie offline
Witaj wykrywanie anomalii i oceny ryzyka hello zdarzenia, takie jak próba logowania po fakcie hello na zdarzenie, która została już wykonana.

### <a name="policy-condition"></a>Stan zasad
Część zasad zabezpieczeń, który definiuje hello jednostek (grup, użytkownicy, aplikacje, platformy urządzeń, Stany urządzeń, zakresy adresów IP, typy klientów) zawartych w zasadach hello lub wykluczone z niego.

### <a name="policy-rule"></a>Reguła zasad
część Hello zasady zabezpieczeń, które opisano hello okoliczności, które spowoduje wywołanie hello zasad i hello akcje podjęte po wyzwoleniu hello zasad.

### <a name="prevention"></a>Zapobieganie
Akcja tooprevent uszkodzenia toohello organizacji za pośrednictwem nadużycia tożsamości lub urządzenia podejrzanych lub znać toobe naruszenia zabezpieczeń. Akcji związanych z zapobieganiem nie zabezpieczyć urządzenia hello lub tożsamości, a nie rozwiązuje poprzednie zdarzenia ryzyka.

### <a name="privileged-user"></a>Uprzywilejowane (użytkownika)
Użytkownik, który w czasie hello zdarzenia ryzyka, ma tooone uprawnienia administratora stałych lub tymczasowych lub więcej zasobów w usłudze Active Directory, takie jak Administrator globalny, Administrator rozliczeń, Administrator usługi, administrator użytkownika i hasło Administrator. 

### <a name="real-time"></a>W czasie rzeczywistym
Zobacz wykrywanie w czasie rzeczywistym.

### <a name="real-time-detection"></a>Wykrywanie w czasie rzeczywistym
Witaj wykrywanie anomalii i oceny ryzyka hello zdarzenia, takie jak prób logowania przed zdarzeniem hello jest dozwolone tooproceed.

### <a name="remediated-risk-event"></a>Skorygowane (ryzyka zdarzenie)
Stan zdarzenia ryzyka ustawione automatycznie ochrony tożsamości i wskazujący, że zdarzenie ryzyka hello korygowania przy użyciu akcji korygowania standardowe powitania dla tego typu zdarzenia ryzyka. Na przykład po zresetowaniu hasła użytkownika hello wiele zdarzeń ryzyka, wskazujące, że zostało naruszone hasło poprzedniej hello są rozwiązywane automatycznie.

### <a name="remediation"></a>Korygowania
Akcja toosecure tożsamości lub urządzeń, które zostały wcześniej podejrzanych lub znane toobe naruszenia zabezpieczeń. Akcja korygowania przywraca hello tożsamości lub urządzenie tooa bezpieczne i usuwa poprzednie zdarzenia ryzyko związane z tożsamości hello lub urządzenia.

### <a name="resolved-risk-event"></a>Rozwiązany (ryzyka zdarzenie)
Stan zdarzenia czynnika ryzyka ustawionych ręcznie przez użytkownika ochronę tożsamości, informujący, że użytkownik hello przejął akcji korygowania odpowiednie poza Identity Protection i zdarzenia ryzyka hello należy traktować jako zamknięte.

### <a name="risk-event-status"></a>Stan zdarzenia ryzyka
Właściwości zdarzenia ryzyka, wskazującą, czy zdarzenia hello jest aktywna oraz czy zamknięte, przyczynę hello jej zamknięcia.

### <a name="risk-event-type"></a>Typ zdarzenia ryzyka
Kategorię hello ryzyko zdarzeń i wskazujący typ hello anomalii powodujący toobe zdarzeń hello uważane za ryzykowne.

### <a name="risk-level-risk-event"></a>Poziom ryzyka (ryzyka zdarzenie)
Wskazanie (wysoki, średni lub niski) ważność hello hello ryzyka zdarzeń toohelp ochronę tożsamości użytkowników priorytetów działań hello podejmują tooreduce hello ryzyka tootheir organizacji. 

### <a name="risk-level-sign-in"></a>Poziom ryzyka (logowanie)
Wskazanie (wysoki, średni lub niski) prawdopodobieństwo hello czy dla określonego logowania, próbuje ktoś toouse hello tożsamości użytkownika.

### <a name="risk-level-user-compromise"></a>Poziom ryzyka (naruszenia zabezpieczeń użytkownika)
Wskazanie (wysoki, średni lub niski) hello prawdopodobieństwo, że naruszono tożsamości.

### <a name="risk-level-vulnerability"></a>Poziom ryzyka (luki w zabezpieczeniach)
Wskazanie (wysoki, średni lub niski) ważność hello hello luki w zabezpieczeniach toohelp ochronę tożsamości użytkowników priorytetów działań hello podejmują tooreduce hello ryzyka tootheir organizacji.

### <a name="secure-identity"></a>Secure (tożsamości)
Podjąć akcję naprawczą, takie jak zmiany hasła lub ponownej instalacji systemu toorestore stanu tooan, który nie został naruszony potencjalnie złamany tożsamości komputera.

### <a name="security-policy"></a>Zasady zabezpieczeń
Kolekcja reguł zasad i warunek. Zasady mogą być zastosowane tooentities, takich jak użytkownicy, grupy aplikacji, urządzeń, platformy urządzeń, Stany urządzeń, zakresy adresów IP i Auth2.0 typy klientów. Gdy jest włączona, zostanie ona potraktowana zawsze, gdy jednostka uwzględniony w zasadach hello jest wystawiony token dla zasobu.

### <a name="sign-in-v"></a>Zaloguj się (v)
tooauthenticate tooan tożsamość w usłudze Azure Active Directory.

### <a name="sign-in-n"></a>Logowania (n)
proces Hello lub akcji uwierzytelniania tożsamości w usłudze Azure Active Directory i hello zdarzeń, który przechwytuje tej operacji.

### <a name="sign-in-from-anonymous-ip-address"></a>Logowania z anonimowych adresów IP
Zdarzenie ryzyka wyzwalane po pomyślnym zalogowaniu z adresu IP, który został zidentyfikowany jako adres IP anonimowy serwer proxy.

### <a name="sign-in-from-infected-device"></a>Logowania z zainfekowanych urządzeń
Wyzwalane, gdy logowania pochodzi z adresu IP, w których jest używany przez co najmniej jedno urządzenie ze złamanymi zabezpieczeniami, które próbujesz aktywnie toocommunicate z serwerem botów toobe zdarzenie ryzyka.

### <a name="sign-in-from-ip-address-with-suspicious-activity"></a>Logowania z adresów IP związanych z podejrzanymi działaniami
Zdarzenie ryzyka wyzwalane po pomyślnym logowanie z adresu IP adresów z dużej liczby nieudanych prób logowania na wielu kontach użytkowników w krótkim przedziale czasu.

### <a name="sign-in-from-unfamiliar-location"></a>Logowania z nieznanych lokalizacji
Zdarzenie ryzyka, wyzwalane, gdy użytkownik pomyślnie loguje się z nowej lokalizacji (adresu IP, szerokości geograficznej/długości i ASN).

### <a name="sign-in-risk"></a>Ryzyko logowania
Zobacz ryzyka poziom (logowanie)

### <a name="sign-in-risk-policy"></a>Zasady logowania ryzyka
Zasady dostępu warunkowego, która ocenia hello ryzyka tooa określonych logowania i stosuje środki zaradcze, na podstawie wstępnie zdefiniowane warunki i zasady.

### <a name="user-compromise-risk"></a>Ryzyko naruszenia zabezpieczeń użytkownika
Zobacz ryzyka poziom (naruszenia zabezpieczeń użytkownika)

### <a name="user-risk"></a>Ryzyko użytkownika
Zobacz ryzyka poziom (naruszenia zabezpieczeń użytkownika).

### <a name="user-risk-policy"></a>Zasady użytkownika ryzyka
Zasady dostępu warunkowego, która uwzględnia logowania hello i stosuje środki zaradcze, na podstawie wstępnie zdefiniowane warunki i zasady.

### <a name="users-flagged-for-risk"></a>Użytkownicy oflagowani w związku z ryzykiem
Użytkownicy, którzy mają zdarzenia ryzyka, które są aktywne lub skorygowanych

### <a name="vulnerability"></a>Luki w zabezpieczeniach
Konfiguracja lub warunku w usłudze Azure Active Directory, dzięki czemu tooexploits wrażliwych katalogu hello lub zagrożenia.

## <a name="see-also"></a>Zobacz też
* [Ochronę tożsamości usługi Azure Active Directory](active-directory-identityprotection.md)

