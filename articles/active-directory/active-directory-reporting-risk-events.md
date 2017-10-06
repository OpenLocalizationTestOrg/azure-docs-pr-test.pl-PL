---
title: "zdarzenia o podwyższonym ryzyku usługi Active Directory aaaAzure | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera szczegółowe omówienie są zdarzenia o podwyższonym ryzyku."
services: active-directory
keywords: "ochronę tożsamości usługi Azure active directory, zabezpieczeń, ryzyka, poziom ryzyka, luki w zabezpieczeniach, zasady zabezpieczeń"
author: MarkusVi
manager: femila
ms.assetid: fa2c8b51-d43d-4349-8308-97e87665400b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d771c1f43707744aac728c4f72000d855cbd6e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-risk-events"></a>Zdarzenia o podwyższonym ryzyku Azure Active Directory

Większość Hello zabezpieczeń potrwać naruszeń miejsce, gdy osoby atakujące uzyskania dostępu do środowiska tooan kradzieży tożsamości użytkownika. Odnajdywanie złamany tożsamości jest bez łatwe zadania. Usługa Azure Active Directory korzysta z adaptacyjną machine learning algorytmów i heurystyki toodetect podejrzane akcji, które są powiązane tooyour kont użytkowników. Każdy wykryto podejrzane działania są przechowywane w rekordzie o nazwie *zdarzenia ryzyka*.

Obecnie usługa Azure Active Directory wykrywa sześć typów zdarzeń o podwyższonym ryzyku:

- [Użytkownicy z ujawnione poświadczenia](#leaked-credentials) 
- [Logowania z anonimowych adresów IP](#sign-ins-from-anonymous-ip-addresses) 
- [Niemożliwa podróż tooatypical lokalizacji](#impossible-travel-to-atypical-locations) 
- [Logowania z nieznanych lokalizacji](#sign-in-from-unfamiliar-locations)
- [Logowania z zainfekowanych urządzeń](#sign-ins-from-infected-devices) 
- [Logowania z adresów IP związanych z podejrzanymi działaniami](#sign-ins-from-ip-addresses-with-suspicious-activity) 


![Zdarzenia ryzyka](./media/active-directory-reporting-risk-events/91.png)

Ten temat zawiera możesz są szczegółowe omówienie jakie zdarzenia o podwyższonym ryzyku i używania ich tooprotect tożsamości usługi Azure AD.


## <a name="risk-event-types"></a>Rodzaje ryzykownych zdarzeń

Właściwość typu zdarzenia ryzyka Hello jest identyfikator hello podejrzane działania rekordu zdarzenia ryzyka została utworzona dla.  
Ciągłe inwestycje firmy Microsoft do procesu wykrywania hello prowadzić do:

- Dokładność wykrywania toohello ulepszenia istniejących zdarzeń ryzyka 
- Nowe typy zdarzeń ryzyka, dodane w przyszłości hello

### <a name="leaked-credentials"></a>Ujawnione poświadczenia

Witaj przestępców komputerowym przestępcom złamania hasła prawidłowy autoryzowanych użytkowników, często udostępnić tych poświadczeń. Zwykle odbywa się przez firmę ich publicznie hello ciemny witryn sieci web i wklejania lub handlem lub sprzedaży hello poświadczeń na powitania czarnym rynku. Witaj Microsoft ujawnione poświadczenia usługi uzyskuje nazwę użytkownika / hasło pary przez monitorowanie publicznego i ciemny witryn sieci web i Praca z:

- Badacze
- Organom ścigania
- Zespoły zabezpieczeń w firmie Microsoft
- Innych zaufanych źródeł. 

Gdy usługa hello wymaga nazwy użytkownika / pary hasła one są porównywane z bieżącym prawidłowe poświadczenia użytkowników usługi AAD. Po znalezieniu dopasowania, oznacza to, że naruszono bezpieczeństwo hasła użytkownika, a *ujawnione poświadczenia ryzyka zdarzeń* jest tworzony.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Logowania z anonimowych adresów IP

Ten typ zdarzenia ryzyka identyfikuje użytkowników, którzy zalogowali się pomyślnie z adresu IP, który został zidentyfikowany jako adres IP anonimowy serwer proxy. Te serwery proxy są używane przez osoby, które mają toohide adres IP swoich urządzeń i może służyć do złośliwymi działaniami.


### <a name="impossible-travel-tooatypical-locations"></a>Niemożliwa podróż tooatypical lokalizacji

Ten typ zdarzenia ryzyka identyfikuje dwa logowania pochodzące z odległymi geograficznie lokalizacji, w którym co najmniej jednej z lokalizacji hello może być również nietypowe dla użytkownika hello, podane poza zachowanie. Ponadto hello czas między hello dwa logowania jest krótszy niż czas hello wszystkich operacji zajęłoby hello tootravel użytkownika z pierwszego toohello lokalizacji hello drugiego, wskazujący, że inny użytkownik korzysta hello sam poświadczeń. 

Tego algorytmu uczenia maszynowego, który ignoruje oczywiste "*fałszywych alarmów*" przyczyniając się toohello niemożliwa podróż warunku, takie jak sieci VPN i lokalizacje regularnie używane przez innych użytkowników w organizacji hello.  Hello system ma okres learning początkowej 14 dni, w których uczy się nowego użytkownika logowania zachowanie.

### <a name="sign-in-from-unfamiliar-locations"></a>Logowania z nieznanych lokalizacji

Ten typ zdarzenia ryzyka uwzględnia poza logowania w lokalizacji (IP, zakres / geograficzne i ASN) toodetermine nowe / nieznanych lokalizacji. Witaj system przechowuje informacje dotyczące powyższych lokalizacjach, używane przez użytkownika i traktuje te lokalizacje "znanych". Hello ryzyka zdarzenie jest wyzwalane, gdy logowania hello występuje z lokalizacji, która nie jest jeszcze hello listę znanych lokalizacji. Hello system ma początkowej learning okres 30 dni, w których nie Flaga wszelkie nowe lokalizacje jako nieznanych lokalizacji. Hello system ignoruje także logowania z urządzeń znanych i lokalizacje, które są od siebie lokalizacjach geograficznych Zamknij tooa znanych lokalizacji. 

### <a name="sign-ins-from-infected-devices"></a>Logowania z zainfekowanych urządzeń

Ten typ zdarzenia ryzyka identyfikuje logowania z urządzeń zainfekowanych złośliwym oprogramowaniem, które są znane tooactively komunikować się z serwerem botów. Jest to określane przez skorelowanie adresów IP hello na urządzeniu użytkownika z adresami IP, które były kontaktu z serwerem botów. 

### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a>Logowania z adresów IP związanych z podejrzanymi działaniami
Ten typ zdarzenia ryzyka identyfikuje adresów IP, z których dużej liczby nieudanych prób logowania były widoczne, na wielu kontach użytkowników w krótkim przedziale czasu. Ruchu jest charakterystyczny dla adresów IP używanych przez osoby atakujące i jest silne wskaźnika, który konta albo są już lub o toobe naruszenia zabezpieczeń. Jest to algorytmu uczenia maszynowego, który ignoruje oczywiste "*alarmów false*", takie jak adresy IP są regularnie używane przez innych użytkowników w organizacji hello.  Hello system ma okres learning początkowej 14 dni, gdzie uczy się hello logowania zachowanie nowego użytkownika i nowej dzierżawy.


## <a name="detection-type"></a>Typ wykrywania

Właściwość type wykrywania Hello są wskaźnikami (w czasie rzeczywistym lub w trybie Offline) dla przedziału czasu wykrywania hello zdarzenia ryzyka.  
Obecnie większość zdarzeń o podwyższonym ryzyku są wykrywane w trybie offline w ramach operacji przetwarzania końcowego po hello ryzyka zdarzenia.

Witaj w poniższej tabeli wymieniono hello ilość czasu potrzebnego dla tooshow typu wykrywania w raporcie pokrewne:

| Typ wykrywania | Opóźnienie raportowania |
| --- | --- |
| W czasie rzeczywistym | 5 too10 minut |
| W trybie offline | 2 too4 godziny |


Dla typów zdarzeń ryzyka hello, które wykrywa usługi Azure Active Directory dostępne są następujące typy wykrywania hello:

| Typ zdarzenia ryzyka | Typ wykrywania |
| :-- | --- | 
| [Użytkownicy z ujawnione poświadczenia](#leaked-credentials) | W trybie offline |
| [Logowania z anonimowych adresów IP](#sign-ins-from-anonymous-ip-addresses) | W czasie rzeczywistym |
| [Niemożliwa podróż tooatypical lokalizacji](#impossible-travel-to-atypical-locations) | W trybie offline |
| [Logowania z nieznanych lokalizacji](#sign-in-from-unfamiliar-locations) | W czasie rzeczywistym |
| [Logowania z zainfekowanych urządzeń](#sign-ins-from-infected-devices) | W trybie offline |
| [Logowania z adresów IP związanych z podejrzanymi działaniami](#sign-ins-from-ip-addresses-with-suspicious-activity) | W trybie offline|


## <a name="risk-level"></a>Poziom ryzyka

Właściwość poziomu ryzyka Hello zdarzenia ryzyko jest wskaźnikiem (wysoki, średni lub niski) hello ważność i zaufania hello zdarzenia ryzyka. Ta właściwość pomaga tooprioritize hello akcje, które należy wykonać. 

ważność Hello zdarzenia ryzyka hello reprezentuje hello siła sygnału hello jako predykcyjne naruszenia tożsamości.  
zaufanie Hello jest wskaźnikiem hello możliwości fałszywych alarmów. 

Na przykład: 

* **Wysoka**: wysokiego zaufania i zdarzenia ryzyka o wysokim znaczeniu. Te zdarzenia są wskaźniki silnej tożsamości użytkownika hello została naruszona poufność, czy kont użytkowników, wpływ na powinny zostać skorygowane natychmiast.

* **Średnia liczba godzin**: o wysokim znaczeniu, ale niższe zdarzeń ryzyka zaufania, albo na odwrót. Te zdarzenia są potencjalnie ryzykowne i kont użytkowników w pełni funkcjonalne należy skorygować.

* **Niski**: małych zaufania i zdarzenia ryzyka o niskim znaczeniu. To zdarzenie może nie wymagać natychmiastowego działania, ale w połączeniu z innymi zdarzeniami ryzyka może zapewnić silne wskazuje, że hello tożsamości jest zagrożone.

![Poziom ryzyka](./media/active-directory-reporting-risk-events/01.png)

### <a name="leaked-credentials"></a>Ujawnione poświadczenia

Ujawnione poświadczenia zdarzenia o podwyższonym ryzyku są sklasyfikowane jako **wysokiej**, ponieważ udostępniają one jednoznacznie zidentyfikować, że hello nazwę użytkownika i hasło są dostępne tooan atakująca.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Logowania z anonimowych adresów IP

Witaj poziom ryzyka dla tego typu zdarzenia ryzyko jest **średni** ponieważ anonimowego adresu IP nie jest oznaczenie silne naruszenia konta.  
Zaleca się natychmiast kontaktu hello tooverify użytkownika za pomocą anonimowych adresów IP.


### <a name="impossible-travel-tooatypical-locations"></a>Niemożliwa podróż tooatypical lokalizacji

Niemożliwa podróż jest zwykle dobry wskaźnik, że haker był się w stanie toosuccessfully. Jednak alarmów false może wystąpić, gdy użytkownik podróżuje przy użyciu nowego urządzenia lub sieci VPN, który zazwyczaj nie jest używany przez innych użytkowników w organizacji hello. Aplikacje, które niepoprawnie przekazywania adresów IP serwera jako adresy IP, które mogą spowodować wygląd powitania klienta jest inne źródło alarmów false rejestrowania znajduje się miejsce z hello centrum danych, gdzie tej aplikacji do wewnętrznego (często są to centrach danych firmy Microsoft, które mogą spowodować wygląd hello logowania spowalniać firmy Microsoft należy adresów IP). W wyniku tych false alarmów hello poziom ryzyka dla tego zdarzenia ryzyko jest **średni**.

> [!TIP]
> Można zmniejszyć ilość hello zgłoszone positves false dla tego typu zdarzenia ryzyko przez skonfigurowanie [o nazwie lokalizacje](active-directory-named-locations.md). 

### <a name="sign-in-from-unfamiliar-locations"></a>Logowania z nieznanych lokalizacji

Nieznanych lokalizacji można podać silne wskazanie, że atakujący jest w stanie toouse kradzieży tożsamości. FALSE alarmów może wystąpić, gdy użytkownik podróżuje, próbuje się nowego urządzenia lub jest za pomocą nowej sieci VPN. W wyniku tych fałszywych alarmów hello poziom ryzyka dla tego typu zdarzenia jest **średni**.

### <a name="sign-ins-from-infected-devices"></a>Logowania z zainfekowanych urządzeń

To zdarzenie ryzyka identyfikuje adresy IP, nie urządzeń użytkownika. Jeśli kilka urządzeń znajdują się za jeden adres IP, a tylko niektóre są kontrolowane przez sieć bot logowania z innymi urządzeniami Moje wyzwalacza to zdarzenie niepotrzebnie, czyli Przyczyna hello klasyfikowania to zdarzenie ryzyka jako **małej**.  

Firma Microsoft zaleca, skontaktuj się z hello użytkownika i skanowanie wszystkich użytkowników hello urządzeń. Istnieje również możliwość, że jest zainfekowany urządzenia osobiste użytkownika lub jak wspomniano wcześniej, że ktoś inny używał zainfekowanego urządzenia z hello sam adres IP użytkownika hello. Zainfekowanych urządzeń są często zainfekowany złośliwym oprogramowaniem, które nie zostały jeszcze zidentyfikowane przez oprogramowanie antywirusowe i może również oznaczać jako płynność zwyczaje, które mogą być przyczyną hello toobecome urządzeń zainfekowanych.

Aby uzyskać więcej informacji o tym, jak tooaddress infekcji złośliwym oprogramowaniem, zobacz hello [Centrum ochrony przed złośliwym oprogramowaniem](http://go.microsoft.com/fwlink/?linkid=335773&clcid=0x409).


### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a>Logowania z adresów IP związanych z podejrzanymi działaniami

Zalecane jest skontaktowanie się hello tooverify użytkownika, gdy faktycznie zarejestrowane w z adresu IP, która została oznaczona jako podejrzana. Hello poziom ryzyka dla tego typu zdarzenia to "**średni**" ponieważ kilka urządzeń mogą znajdować się za hello tego samego adresu IP, gdy tylko niektóre mogą być odpowiedzialne za hello podejrzanych działań. 


 
## <a name="next-steps"></a>Następne kroki

Zdarzenia o podwyższonym ryzyku są foundation hello ochrony tożsamości usługi Azure AD. Usługi Azure AD można obecnie wykrywa sześciu zdarzenia ryzyka: 


| Typ zdarzenia ryzyka | Poziom ryzyka | Typ wykrywania |
| :-- | --- | --- |
| [Użytkownicy z ujawnione poświadczenia](#leaked-credentials) | Wysoka | W trybie offline |
| [Logowania z anonimowych adresów IP](#sign-ins-from-anonymous-ip-addresses) | Medium | W czasie rzeczywistym |
| [Niemożliwa podróż tooatypical lokalizacji](#impossible-travel-to-atypical-locations) | Medium | W trybie offline |
| [Logowania z nieznanych lokalizacji](#sign-in-from-unfamiliar-locations) | Medium | W czasie rzeczywistym |
| [Logowania z zainfekowanych urządzeń](#sign-ins-from-infected-devices) | Niska | W trybie offline |
| [Logowania z adresów IP związanych z podejrzanymi działaniami](#sign-ins-from-ip-addresses-with-suspicious-activity) | Medium | W trybie offline|

Gdzie można znaleźć hello zdarzenia ryzyka, które zostały wykryte w danym środowisku?
Istnieją dwa miejsca, w którym przejrzeć zdarzenia zgłoszone ryzyka:

 - **Raportowanie na platformie Azure AD** -zdarzenia o podwyższonym ryzyku są częścią zabezpieczeń usługi Azure AD raportów. Aby uzyskać więcej informacji, zobacz hello [użytkowników na zagrożenia bezpieczeństwa raport](active-directory-reporting-security-user-at-risk.md) i hello [raport zabezpieczeń ryzykowne logowania](active-directory-reporting-security-risky-sign-ins.md).

 - **Azure AD Identity Protection** -zdarzenia o podwyższonym ryzyku są również częścią [Azure Active Directory Identity Protection](active-directory-identityprotection.md) funkcje raportowania.
    

Gdy hello wykrycie zdarzenia o podwyższonym ryzyku już reprezentuje istotnym elementem ochrony Twojej tożsamości, masz również hello opcja tooeither ręcznie rozwiązać je lub nawet implementację automatyczne odpowiedzi przez skonfigurowanie zasad dostępu warunkowego. Aby uzyskać więcej informacji, zobacz z [Azure Active Directory Identity Protection](active-directory-identityprotection.md).
 
