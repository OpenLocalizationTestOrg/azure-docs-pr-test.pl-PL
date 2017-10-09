---
title: "Usługa Azure Active Directory B2C: Odwołanie - zaufania struktur | Dokumentacja firmy Microsoft"
description: "Temat dotyczący zasad niestandardowych usługi Azure Active Directory B2C i hello Framework obsługi tożsamości"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: d9634da72cb136ac165dd32e735622b5d0e22ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="define-trust-frameworks-with-azure-ad-b2c-identity-experience-framework"></a>Definiowanie relacji zaufania platformy Framework obsługi tożsamości usługi Azure AD B2C

Usługa Azure Active Directory B2C (Azure AD B2C) zasad niestandardowych, które używają hello Framework obsługi tożsamości Podaj organizacji za pomocą scentralizowanej usługi. Ta usługa pozwala ograniczyć złożoność hello federacji tożsamości w dużych społeczności zainteresowań. złożoność Hello jest zmniejszenie tooa pojedynczą relacją zaufania i wymiany metadanych pojedynczego.

Azure AD B2C niestandardowych zasad używających hello tooenable Framework obsługi tożsamości możesz tooanswer hello następujące pytania:

- Co to są hello prawnych, zabezpieczeń, prywatności i zasady ochrony danych, które należy przestrzegać?
- Kim są hello kontaktów i jakie procesy hello staje się akredytowanego uczestnika?
- Kim są hello akredytowane dostawców informacji o tożsamości (znanej także jako "dostawców oświadczeń") i jakie są one oferowane?
- Kim są hello akredytowane uzależnionych (i opcjonalnie, co to są one wymagane)?
- Co to są techniczne "umieszczonego powitania" hello wymagania dotyczące współdziałania dla uczestników?
- Co to są reguły operational "runtime" hello, które muszą zostać wymuszone wymiany informacji o tożsamości cyfrowych?

tooanswer skonstruować wszystkie te pytania, zasad niestandardowych usługi Azure AD B2C, które używają hello Framework obsługi tożsamości Użyj hello zaufania Framework (TF). Zastanówmy się, że ta konstrukcja i go zawiera.

## <a name="understand-hello-trust-framework-and-federation-management-foundation"></a>Zrozumienie hello Framework zaufania i Federacji management foundation

Hello zaufania Framework jest specyfikacją napisane hello tożsamości, zabezpieczeń, prywatności oraz danych ochrony zasad, które toowhich uczestnicy społeczności zainteresowania muszą być zgodne.

Tożsamości federacyjnych stanowi podstawę do osiągnięcia weryfikacji tożsamości użytkownika końcowego na dużą skalę Internet. Przez delegowanie tożsamości zarządzania toothird stron, wiele jednostek uzależnionych mogą być używane jednej tożsamości cyfrowych dla użytkownika końcowego.  

Weryfikacji tożsamości wymaga, aby atrybut dostawców (AtPs) i dostawcy tożsamości (IdPs) jest zgodna toospecific zabezpieczeń, ochrony prywatności i operacyjne zasady i praktyki dotyczące.  Jeśli nie mogą wykonywać bezpośredniej kontroli, jednostki uzależnione (RPs) należy opracować relacji zaufania z hello IdPs i AtPs wybiera on toowork z.  

Miarę zwiększania się liczby hello konsumenci i dostawcy tożsamości cyfrowych informacji jest trudne toocontinue zarządzania parowania tych relacji zaufania, lub nawet hello parowania wymiany metadanych techniczne hello, która jest wymagana do obsługi łączności sieciowej .  Koncentratory federacyjnego zostały osiągnięte tylko ograniczone sukces w rozwiązywaniu tych problemów.

### <a name="what-a-trust-framework-specification-defines"></a>Definiuje specyfikacji Framework zaufania
TFs są linchpins hello hello Framework zaufania Otwórz tożsamości programu Exchange (OIX) modelu, gdzie społeczności każdej istotnej podlega warunkom określonym specyfikacji TF. Definiuje specyfikację TF:

- **Witaj zabezpieczenia i prywatność metryki dla społeczności hello płynących z definicją hello:**
    - Witaj poziomy ubezpieczenia (LOA), które są oferowane/wymagane przez uczestników; na przykład, uporządkowany zestaw zaufania klasyfikacje hello autentyczności informacji o tożsamości cyfrowych.
    - Witaj poziomów ochrony (LOP), które są oferowane/wymagane przez uczestników; na przykład, uporządkowany zestaw zaufania klasyfikacje hello ochrony informacji tożsamości cyfrowych, który jest obsługiwany przez uczestnicy społeczności hello odsetek.

- **Witaj opis informacji tożsamości cyfrowych hello, który ma oferowana wymagane przez uczestników**.

- **Zasady techniczne Hello produkcji i zużycia informacji o tożsamości cyfrowych, a zatem pomiaru LOA i LOP. Obejmują one zapisane zasad zwykle hello następujące kategorie zasad:**
    - Tożsamość sprawdzania zasad, na przykład: *jak silnie jest sprawdzane informacje o tożsamości osoby?*
    - Zasady zabezpieczeń, na przykład: *jak silnie są informacje o integralności i poufności chronione?*
    - Zasady zachowania poufności informacji, na przykład: *jakie kontrolki użytkownika ma za pośrednictwem dane osobowe (dane osobowe)*?
    - Zasady przeżywalność, na przykład: *Jeśli dostawca przestaje operacje, jak ciągłości i ochrony danych osobowych funkcji?*

- **Profile techniczne Hello produkcji i zużycia informacji o tożsamości cyfrowych. Takie profile zawierają:**
    - Zakres interfejsy, dla których jest dostępna w określonym LOA informacji o tożsamości cyfrowych.
    - Wymagania techniczne dotyczące współdziałania o transmisji.

- **opisy Hello hello różne role uczestnicy społeczności hello może wykonywać i hello kwalifikacji, które są wymagane toofulfill tych ról.**

W związku z tym specyfikacji TF kontroluje sposób wymiany informacji o tożsamości między uczestnikami hello społeczności hello zainteresowania: uzależnionych, tożsamości i dostawców atrybut i atrybut weryfikatory.

Specyfikacja TF jest jednym lub wieloma dokumentami służących jako punkt odniesienia dla zarządu hello społeczności hello odsetek reguluje hello potwierdzenia i zużycia tożsamości cyfrowych informacji w ramach społeczności hello. Jest udokumentowany zestawu zasad i procedur zaprojektowany tooestablish zaufania hello tożsamości cyfrowych, które są używane w transakcji internetowych między członkami społeczności odsetek.  

Innymi słowy Specyfikacja TF definiuje reguły hello tworzenie ekosystemu działało tożsamości federacyjnych dla społeczności.

Obecnie jest powszechnie zgody na powitania korzyści takie podejście. Brak bez wątpienia który specyfikacje framework ułatwienia hello projektowanie tożsamości cyfrowych ekosystemu zweryfikowania właściwości zabezpieczeń, bezpieczeństwa i ochrony prywatności, co oznacza, że może być ponownie między kilka Wspólnot odsetek zaufania.

Z tego powodu zasad niestandardowych usługi Azure AD B2C, które używają hello Framework obsługi tożsamości używa specyfikacji hello jako podstawa hello jej reprezentacji danych współdziałania toofacilitate TF.  

Azure zasady niestandardowe AD B2C, korzystających z hello Framework obsługi tożsamości reprezentują specyfikacji TF jako kombinacja odczytania przez człowieka i danych. Niektóre sekcje w tym modelu (zazwyczaj sekcje, które są bardziej opracowane głównie pod kątem zarządzania) są reprezentowane jako odwołuje się do dokumentacji toopublished zabezpieczenia i prywatność zasad wraz z hello dotyczące procedur (jeśli istnieje). Pozostałe sekcje opisują szczegółów hello metadanych i środowiska uruchomieniowego reguły konfiguracji ułatwiających operacyjne automatyzacji.

## <a name="understand-trust-framework-policies"></a>Zrozumieć zasady zaufania Framework

W implementacji hello specyfikacji TF składa się z zestawu zasad, umożliwiające pełną kontrolę nad zachowania tożsamości i środowiska.  Azure AD B2C niestandardowych zasad korzystających z hello Framework obsługi tożsamości tooauthor należy włączyć i tworzyć własne TF za pomocą takich deklaratywne zasad, które można zdefiniować i skonfigurować:

- odwołania dokumentu Hello lub odwołań, definiujące ekosystemu tożsamości federacyjnych hello hello społeczności, który dotyczy toohello TF. Są one łącza toohello TF dokumentacji. Witaj reguły (wstępnie zdefiniowane) operational "runtime" lub hello podróże użytkownika, które zautomatyzować i/lub kontrolować hello programu exchange i użycia hello oświadczeń. Te podróże użytkowników są skojarzone z LOA (i LOP). Zasady mogą więc podróże użytkownika ze zróżnicowanymi LOAs (i LOPs).

- dostawcy tożsamości i atrybut Hello lub hello dostawców oświadczeń, społeczności hello odsetek i hello profilów techniczne obsługują wraz z hello akredytacji LOA/LOP (poza pasmem), które odnoszą się toothem.

- Integracja Hello weryfikatory atrybutu lub dostawców oświadczeń.

- Witaj w hello społeczności jednostek uzależnionych (za pomocą wnioskowania).

- metadane Hello ustalania komunikacji sieciowej między uczestników. Te metadane, wraz z hello techniczne profile, są używane podczas tooplumb transakcji "umieszczonego hello" współdziałanie hello jednostki uzależnionej, a inni uczestnicy społeczności.

- Witaj konwersji protokołu, jeśli istnieją (na przykład SAML, OAuth2, WS-Federation i OpenID Connect).

- wymagania dotyczące uwierzytelniania Hello.

- Witaj wieloskładnikowego aranżacji ewentualne.

- Udostępniony schemat dla wszystkich hello oświadczenia, które są dostępne i mapowania tooparticipants społeczności odsetek.

- Witaj wszystkich oświadczeń przekształcenia wraz z hello minimalizacja danych w tym kontekście, toosustain hello exchange i użycia hello oświadczeń.

- Powiązanie Hello i szyfrowania.

- Witaj oświadczeń magazynu.

### <a name="understand-claims"></a>Zrozumienie oświadczeń

> [!NOTE]
> Firma Microsoft zbiorczo można znaleźć tooall hello możliwych typów informacji o tożsamości, które mogą być wymieniane jako "oświadczenia": oświadczeń o poświadczenie uwierzytelnienia użytkownika końcowego, czasie głosowania nad tożsamości, urządzenia komunikacji, lokalizacji fizycznej, umożliwiających zidentyfikowanie atrybuty i tak dalej.  
>
> Możemy użyć hello termin "oświadczenia"--zamiast "attributes"--, ponieważ w transakcji w trybie online tych artefaktów danych nie są fakty, które można bezpośrednio sprawdzić przez hello jednostki zależnej. A nie są one potwierdzeń lub oświadczeń o faktów, które hello jednostki uzależnionej należy opracować transakcji żądanych wystarczające zaufania toogrant hello przez użytkownika końcowego.  
>
> Używamy hello termin "oświadczenia" ponieważ usługi Azure AD B2C są zasady niestandardowe, które używają hello Framework obsługi tożsamości exchange hello toosimplify wszystkich typów informacji o tożsamości cyfrowych w sposób ciągły, niezależnie od tego, czy hello podstawowy Protokół jest zdefiniowany dla pobierania atrybut lub uwierzytelniania użytkownika.  Podobnie używamy hello termin "dostawców oświadczeń" toocollectively można znaleźć tooidentity dostawców, dostawców atrybut i atrybut weryfikatory podczas nie chcemy toodistinguish między określonych funkcji.   

W związku z tym określają one, jak informacje o tożsamości są wymieniane między uzależniona, tożsamości i dostawców atrybut i atrybut weryfikatory. Decydować, tożsamość i dostawców atrybut są wymagane do uwierzytelniania jednostką uzależnioną. Powinny zostać uznane jako języka specyficznego dla domeny (DSL), czyli języku komputera, który ma przeznaczone do domeny określonej aplikacji z dziedziczenia, *Jeśli* instrukcje, polimorfizm.

Zasady te stanowią hello czytelną część hello TF skonstruować w zasadach niestandardowych usługi Azure AD B2C wykorzystaniu hello Framework obsługi tożsamości. Obejmują wszystkie szczegóły operacyjne hello, w tym dostawców oświadczeń metadanych i profile technicznych, definicje schematów oświadczeń funkcji przekształcania oświadczeń i podróże użytkownika, które są wypełnione w toofacilitate operacyjne aranżacji i Automatyzacja.  

Są one przyjęto toobe *dokumenty życia* ponieważ istnieje szansa, że ich zawartość zmieni się wraz z upływem czasu dotyczących aktywnych uczestników hello zadeklarowany w hello zasad. Istnieje również ryzyko hello hello warunków i postanowień jest uczestnika mogą ulec zmianie.  

Federacyjnego instalacja i konserwacja znacząco są uproszczone dzięki uzależnione od bieżących reconfigurations zaufania i łączność osłony, jak różne oświadczenia dostawców/weryfikatory join lub pozostaw (reprezentowane przez społeczność hello) hello zestaw zasad.

Inne wyzwanie istotne jest współdziałanie. Dodatkowe oświadczenia dostawców/weryfikatory muszą być zintegrowane, ponieważ toosupport prawdopodobnie nie są uzależnione hello wszystkie niezbędne protokołów. Niestandardowe zasady usługi Azure AD B2C rozwiązać ten problem dzięki obsłudze standardowych protokołów i stosując podróże określonego użytkownika tootranspose żądania, gdy nie obsługują jednostek uzależnionych i dostawców atrybut hello tego samego protokołu.  

Podróże użytkownika obejmują profile protokołu i metadanych, które są używane tooplumb "umieszczonego hello" współdziałanie hello jednostki uzależnionej i innych uczestników. Istnieją reguły operacyjne środowiska uruchomieniowego, które są komunikaty żądania/odpowiedzi wymiany informacji zastosowane tooidentity wymuszania zgodności z zasadami opublikowanych jako część hello TF specyfikacji. pomysł Hello podróży użytkownika jest klucza toohello dostosowywania hello obsługi klienta. On również rzucają światła na działanie systemu hello na poziomie protokołu hello.

Na tej podstawie portale i aplikacje producentów jednostki uzależnionej w zależności od ich kontekście wywołać zasad niestandardowych usługi Azure AD B2C, że korzystaj z hello Framework obsługi tożsamości przekazywanie hello nazwy określone zasady i uzyskać dokładne zachowanie hello i informacji Exchange, które mają bez żadnego muss problemów i ryzyka.
