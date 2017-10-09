---
title: "Usługi Azure Active Directory B2C: Niestandardowe zasady | Dokumentacja firmy Microsoft"
description: "Temat dotyczący zasad niestandardowych usługi Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1ff398a4-2079-4615-94f1-57de22c0aad6
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: bada9cf5f1a86f3dd047536f6fd9359c0231a384
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-custom-policies"></a>Usługi Azure Active Directory B2C: Zasady niestandardowe

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

## <a name="what-are-custom-policies"></a>Co to są zasady niestandardowe?

Zasady niestandardowe są pliki konfiguracji, które określają zachowanie hello dzierżawy usługi Azure AD B2C. Podczas gdy **wbudowane zasady** są wstępnie zdefiniowane w portalu usługi Azure AD B2C hello hello najbardziej typowych zadań tożsamości, niestandardowych zasad może być całkowicie zmieniony przez toocomplete developer tożsamości near nieograniczoną liczbę zadań. Zasady niestandardowe są odpowiedniej dla Ciebie i Twojego scenariusza z tożsamością czytać na toodetermine.

**Edytowanie zasad niestandardowych nie jest dla wszystkich użytkowników.** wymagający Hello naukę czas uruchamiania hello jest dłuższy, a przyszłe zmiany toocustom zasad będzie wymagać podobnych toomaintain wiedzy. Wbudowane zasady powinny być starannie przemyślane, najpierw dla danego scenariusza przed użyciem zasad niestandardowych.

## <a name="comparing-built-in-policies-and-custom-policies"></a>Porównywanie wbudowane i niestandardowe zasady

| | Wbudowane zasady | zasady niestandardowe |
|-|-------------------|-----------------|
|Użytkownicy docelowi | Wszystkie deweloperzy aplikacji z lub bez wiedzy tożsamości | Specjaliści tożsamości: integratorów systemów. platforma, konsultantów i zespoły wewnętrznych tożsamości. Potrafisz przepływów OpenIDConnect i zrozumieć dostawców tożsamości i uwierzytelniania opartego na oświadczeniach |
|Metody konfiguracji | Portal Azure przy użyciu przyjaznych dla użytkownika interfejsu użytkownika | Bezpośredniego edytowania plików XML, a następnie przekazywanie toohello portalu Azure |
|Dostosowywanie interfejsu użytkownika | Pełne dostosowywanie interfejsu użytkownika, w tym HTML, CSS i jscript obsługi (wymaga domeny niestandardowej)<br><br>Obsługa wielu języków z ciągami niestandardowe | tym samym |
| Dostosowywanie atrybutu | Standardowe i niestandardowe atrybuty | tym samym |
|Token i sesji zarządzania | Niestandardowy token i wiele opcji sesji | tym samym |
|Dostawców tożsamości| **Dzisiaj**: wstępnie zdefiniowane lokalne, społecznościowych dostawcy<br><br>**Przyszłe**: OAuth opartych na standardach OIDC SAML, | **Dzisiaj**: SAML opartych na standardach OIDC OAUTH,<br><br>**Przyszłe**: WsFed |
|Zadania tożsamości (przykłady) | Uaktywnij lub logowania z wielu kont społecznościowych i lokalne<br><br>Samoobsługowe resetowanie haseł<br><br>Edycja profilu<br><br>Scenariusze uwierzytelniania wieloskładnikowego<br><br>Dostosowywanie tokeny i sesji<br><br>Przepływ tokenu dostępu | Zakończenie hello same zadania jako wbudowanych zasad przy użyciu dostawcy tożsamości niestandardowej lub użyj zakresy niestandardowe<br><br>Ustanów użytkownika w innym systemie w czasie hello rejestracji<br><br>Wysyłania powitalnej wiadomości e-mail, przy użyciu własnego dostawcę usługi poczty e-mail<br><br>Użyj magazynu użytkowników spoza B2C<br><br>Sprawdzanie poprawności użytkownika informacje z zaufanego systemu za pomocą interfejsu API |

## <a name="policy-files"></a>Pliki zasad

Zasady niestandardowe jest reprezentowany jako jeden lub kilka plików w formacie XML, które można znaleźć tooeach innych w łańcuchu hierarchicznej. Zdefiniuj Hello elementów XML: schemat oświadczeń oświadczeń przekształcenia, definicje zawartości profile technical/dostawców oświadczeń i Userjourney aranżacji kroków, między innymi elementami.

Firma Microsoft zaleca użycie hello trzech typów plików zasad:

- **PODSTAWOWY plik**, który zawiera większość hello definicje i dla którego platforma Azure udostępnia kompletnego przykładu.  Zaleca się wprowadzeniu minimalną liczbę zmian toothis pliku toohelp w rozwiązywaniu problemów i długoterminowej konserwacji zasad
- **plik rozszerzenia** przechowuje hello zmian konfiguracji unikatowy dla dzierżawy
- **plik strony jednostki uzależnionej (RP)** czyli hello jednym fokus zadania pliku, który jest wywoływany bezpośrednio przez hello aplikacji lub usługi (alias uzależniona).  Przeczytaj artykuł hello na definicje pliku zasad, aby uzyskać więcej informacji.  Każde zadanie unikatowy wymaga własnego planu odzyskiwania i w zależności od wymagań znakowania hello liczba może być "Całkowita liczba aplikacji x liczba przypadków użycia".


Wbudowane zasady w usłudze Azure AD B2C, wykonaj wzorzec pliku 3 hello przedstawione powyżej, ale Deweloper hello tylko widzi hello pliku jednostki uzależnionej strony (RP), podczas gdy hello portal wprowadza zmiany w pliku EXTenstions toohello tła hello.

## <a name="core-concepts-you-should-know-when-using-custom-policies"></a>Podstawowe koncepcje, których należy wiedzieć, korzystając z zasad niestandardowych

### <a name="azure-active-directory-b2c"></a>Azure Active Directory B2C

Przez klienta tożsamości i dostępu do usługi Azure management (CIAM). Usługa Hello obejmuje:

1. Katalog użytkownika w postaci hello specjalnych usługi Azure Active Directory dostępne za pośrednictwem programu Microsoft Graph, które przechowuje dane użytkownika dla kont lokalnych i kont federacyjnych 
2. Dostęp do toohello **Framework obsługi tożsamości** co organizuje relacji zaufania między użytkowników i jednostek i przekazuje oświadczeń między nimi toocomplete zadanie zarządzania tożsamościami/dostęp 
3. Usługa tokenu zabezpieczającego (STS) wystawiania identyfikator tokenów, Odśwież tokenów i dostępu tokeny (i równoważne potwierdzenia SAML) i weryfikacji ich tooprotect zasobów.

Usługa Azure AD B2C współdziała z dostawców tożsamości, użytkowników i innych systemach i z hello użytkownika lokalnego katalogu w tooachieve sekwencji zadań tożsamości (np. nazwy logowania użytkownika, zarejestrować nowego użytkownika, resetowanie hasła). Witaj podstawowej platformy, które ustanawia relację zaufania wieloosobową i wykonuje następujące czynności jest wywoływana hello Framework obsługi tożsamości i zasad (nazywanych również przebieg użytkownika lub zasad framework zaufania) jawnie definiuje hello złośliwych użytkowników, akcje hello hello protokoły i hello sekwencji toocomplete czynności.

### <a name="identity-experience-framework"></a>Platforma obsługi tożsamości

Formatuje pełni konfigurowalne, oparte na zasadach, oparte na chmurze platformy Azure, będąca aranżacją relacji zaufania między jednostkami (szeroko dostawców oświadczeń) w standardowego protokołu OpenIDConnect, OAuth, SAML, WSFed i kilka z nich niestandardowych (np. interfejsu API REST na podstawie System — system oświadczeń wymiany). Witaj I2E tworzy przyjazną dla użytkownika, napotyka whitelabelled, który obsługuje HTML, CSS i jscript.  Obecnie hello Framework obsługi tożsamości jest dostępna tylko w kontekście hello hello usługi Azure AD B2C i priorytety dla tooCIAM powiązanych zadań.

### <a name="built-in-policies"></a>Wbudowane zasady

Wstępnie zdefiniowane pliki konfiguracji, że zachowanie bezpośredniego hello Azure AD B2C tooperform hello najczęściej używane tożsamości zadania (tj. Rejestracja użytkownika, rejestrowanie, resetowania hasła) i interakcji z zaufane strony, których relację również wstępnie zdefiniowane w usłudze Azure AD B2C ( np. usługi Facebook dostawcy tożsamości, LinkedIn, Account firmy Microsoft, konta Google).  W przyszłości hello wbudowane zasady mogą również przewidzieć dostosowania dostawców tożsamości, które są zazwyczaj hello obszaru przedsiębiorstwa, np. Azure Active Directory Premium, Active Directory/ADFS Salesforce identyfikator dostawcy.


### <a name="custom-policies"></a>zasady niestandardowe

Pliki konfiguracji definiujące zachowanie hello platformy obsługi tożsamości w dzierżawie usługi Azure AD B2C. Zasady niestandardowe jest dostępny jako jeden lub kilka plików XML (zobacz pliki zasad definicje) wykonywanych przez hello tożsamości środowiska Framework po wywołaniu przez jednostkę uzależnioną (np. aplikacji). Zasady niestandardowe można edytowane bezpośrednio przez toocomplete developer tożsamości near nieograniczoną liczbę zadań. Deweloperzy Konfigurowanie niestandardowych zasad musi definiować hello zaufanych relacje w punkty końcowe metadanych tooinclude szczegółów dokładne, dokładne oświadczeń wymienić definicje i skonfigurować klucze tajne, klucze i certyfikaty, zgodnie z potrzebami każdego dostawcy tożsamości.

## <a name="policy-file-definitions-for-identity-experience-framework-trustframeworks"></a>Definicje pliku zasad dla Trustframeworks Framework obsługi tożsamości

### <a name="policy-files"></a>Pliki zasad

Zasady niestandardowe jest reprezentowany jako jeden lub kilka plików w formacie XML, które można znaleźć tooeach innych w łańcuchu hierarchicznej. Zdefiniuj Hello elementów XML: schemat oświadczeń oświadczeń przekształcenia, definicje zawartości profile technical/dostawców oświadczeń i Userjourney aranżacji kroków, między innymi elementami.  Firma Microsoft zaleca użycie hello trzech typów plików zasad:

- **PODSTAWOWY plik**, który zawiera większość hello definicje i dla którego platforma Azure udostępnia kompletnego przykładu.  Zaleca się wprowadzeniu minimalną liczbę zmian toothis pliku toohelp w rozwiązywaniu problemów i długoterminowej konserwacji zasad
- **plik rozszerzenia** przechowuje hello zmian konfiguracji unikatowy dla dzierżawy
- **plik strony jednostki uzależnionej (RP)** czyli hello jednym fokus zadania pliku, który jest wywoływany bezpośrednio przez hello aplikacji lub usługi (alias uzależniona).  Przeczytaj artykuł hello na definicje pliku zasad, aby uzyskać więcej informacji.  Każde zadanie unikatowy wymaga własnego planu odzyskiwania i w zależności od wymagań znakowania hello liczba może być "Całkowita liczba aplikacji x liczba przypadków użycia".

![Typy zasad](media/active-directory-b2c-overview-custom/active-directory-b2c-overview-custom-policy-files.png)

| Typ pliku zasad | Nazwa pliku przykłady | Zalecane użycie | Dziedziczy |
|---------------------|--------------------|-----------------|---------------|
| PODSTAWA |TrustFrameworkBase.xml<br><br>Mytenant.onmicrosoft.com-B2C-1A_BASE1.xml | Obejmuje hello core oświadczeń schematu, przekształcenia oświadczeń, dostawców oświadczeń i podróże użytkownika skonfigurowane przez firmę Microsoft<br><br>Plik toothis minimalne zmiany | Brak |
| Rozszerzenia (EXT) | TrustFrameworkExtensions.xml<br><br>Mytenant.onmicrosoft.com-B2C-1A_EXT.xml | Konsolidacja zmiany toohello podstawowego pliku w tym miejscu<br><br>Dostawców oświadczeń zmodyfikowane<br><br>Podróże zmodyfikowanego użytkownika<br><br>Definicje własnych niestandardowych schematów | Pliku podstawowego |
| Jednostka uzależniona (RP) | B2C_1A_sign_up_sign_in.XML| Ustawienia tokenu kształt i sesji tutaj| Plik Extensions(ext) |

### <a name="inheritance-model"></a>Model dziedziczenia

Po uruchomieniu pliku zasad RP hello, hello Framework obsługi tożsamości w B2C Dodaj wszystkie elementy hello z podstawowego, a następnie z ROZSZERZEŃ i w końcu z hello RP zasad pliku tooassemble hello bieżące zasady obowiązujące.  Elementy hello sam typ i nazw w pliku RP hello zastępują hello rozszerzenia i zastąpienia rozszerzenia BASE.

**Wbudowane zasady** w usłudze Azure AD B2C należy wykonać opisane powyżej, ale Deweloper hello tylko widzi hello pliku jednostki uzależnionej strony (RP), podczas gdy hello portal wprowadza zmiany w pliku EXTenstions toohello tła hello wzorzec pliku 3 hello.  Wszystkie usługi Azure AD B2C udostępnia podstawowe zasady plik jest pod kontrolą hello zespołu hello Azure B2C jest często aktualizowana.
