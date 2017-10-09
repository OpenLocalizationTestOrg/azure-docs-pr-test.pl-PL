---
title: "aaaAzure ochronę tożsamości w usłudze Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Azure AD Identity Protection umożliwia zdolność hello toolimit tooexploit osoba atakująca, którego bezpieczeństwo zostało naruszone tożsamości lub urządzenie i toosecure tożsamości lub urządzenia, które wcześniej były toobe podejrzenia lub znanych naruszenia zabezpieczeń."
services: active-directory
keywords: "ochronę tożsamości usługi Azure active directory, usługa cloud app discovery, zarządzanie aplikacjami, zabezpieczeń, ryzyka, poziom ryzyka, luki w zabezpieczeniach, zasady zabezpieczeń"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a>Ochrona tożsamości w usłudze Azure Active Directory

Azure Active Directory Identity Protection to funkcja wersji hello Azure AD Premium P2, które umożliwia:

- Wykrywanie potencjalnych luk w zabezpieczeniach wpływających na tożsamości organizacji

- Skonfiguruj automatyczne odpowiedzi toodetected podejrzane akcji, które są powiązane tooyour organizacji tożsamości  

- Zbadaj podejrzane zdarzenia i podejmij odpowiednią akcję tooresolve je   


## <a name="getting-started"></a>Wprowadzenie

Firma Microsoft zabezpiecza oparte na chmurze tożsamości przez ponad dekadę. Z usługi Azure Active Directory Identity Protection, w danym środowisku, możesz użyć hello korzysta z tej samej ochrony systemy Microsoft toosecure tożsamości.

Większość Hello zabezpieczeń potrwać naruszeń miejsce, gdy osoby atakujące uzyskania dostępu do środowiska tooan kradzieży tożsamości użytkownika. Latach hello osoby atakujące stały się coraz bardziej skuteczne w wykorzystaniu naruszeń innych firm i za pomocą zaawansowanej wyłudzania. Gdy osoba atakująca uzyska dostęp do konta użytkownika uprzywilejowanego niskiego tooeven, są one względnie łatwe im dostęp do toogain tooimportant zasobów firmowych za pośrednictwem penetracji sieci.

W wyniku tego należy:

- Ochrona wszystkich tożsamości, niezależnie od ich poziom uprawnień

- Aktywne uniemożliwić złamany tożsamości są użyte

Odnajdywanie złamany tożsamości jest bez łatwe zadania. Azure Active Directory korzysta z algorytmów uczenia maszynowego adaptacyjną i nieprawidłowości toodetect Algorytm heurystyczny i podejrzane zdarzenia, które wskazują potencjalnie naruszony tożsamości. Przy użyciu tych danych, Identity Protection generuje raporty i alerty, które umożliwiają tooevaluate hello wykrytych problemów i podjąć odpowiednie środki zaradcze lub akcji korygowania.

Azure Active Directory Identity Protection jest większa niż monitorowania i raportowania narzędzia. tooprotect tożsamości organizacji, można skonfigurować zasady stosowane na podstawie ryzyka odpowiadające automatycznie toodetected problemów, gdy zostanie osiągnięty poziom ryzyka określony. Te zasady dodatkowo tooother warunkowy dostęp do formantów zapewniane przez usługę Azure Active Directory i EMS, można automatycznie blokować lub zainicjować akcji korygowania adaptacyjną tym resetowanie haseł i wymuszania uwierzytelnianie wieloskładnikowe.


#### <a name="identity-protection-capabilities"></a>Funkcje ochrony tożsamości

**Wykrywanie luk w zabezpieczeniach i ryzykowne kont:**  

* Udostępnia zalecenia niestandardowych tooimprove ogólny stan zabezpieczeń przez wyróżnianie luk w zabezpieczeniach
* Obliczanie poziomów ryzyka do logowania
* Obliczanie poziomów ryzyka użytkownika


**Badanie zdarzenia ryzyka:**

* Wysyłanie powiadomienia o zdarzeniach ryzyka
* Badania ryzyka zdarzeń za pomocą odpowiednich i kontekstowych informacji
* Zapewnienie podstawowych przepływów pracy dochodzenia tootrack
* Zapewniając łatwy dostęp tooremediation akcji, takich jak Resetowanie hasła

**Zasady dostępu warunkowego opartego na ryzyka:**

* Zasady toomitigate ryzykowne logowania przez blokowanie logowania lub wymaganie uwierzytelniania wieloskładnikowego wyzwania.
* Zasady tooblock lub kont użytkowników ryzykowne bezpieczne
* Zasady toorequire użytkowników tooregister uwierzytelnianie wieloskładnikowe



## <a name="identity-protection-roles"></a>Role ochrony tożsamości

tooload saldo hello działania związane z zarządzaniem wokół implementacji ochronę tożsamości, można przypisać kilku ról. Azure AD Identity Protection obsługuje 3 role katalogu:

| Rola                         | Możliwość                          | Nie można wykonać
| :--                          | ---                                |  ---   |
| Administrator globalny         | Pełny dostęp tooIdentity ochrony, dołączyć Identity Protection| |
| Administrator zabezpieczeń       | Pełny dostęp tooIdentity ochrony | Dołączyć ochronę tożsamości, zresetuj hasła dla użytkownika |
| Czytelnik zabezpieczeń              | Dostęp tylko do gotowe tooIdentity ochrony | Dołączyć ochronę tożsamości użytkowników remidiate skonfigurować zasady, resetowania haseł |




Aby uzyskać więcej informacji, zobacz [przypisywanie ról administratorów w usłudze Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)



## <a name="detection"></a>Wykrywanie

### <a name="vulnerabilities"></a>Luki w zabezpieczeniach

Azure Active Directory Identity Protection analizy konfiguracji i wykrywa luk w zabezpieczeniach, które mogą mieć wpływ na tożsamości użytkownika. Aby uzyskać więcej informacji, zobacz [luk w zabezpieczeniach wykrywanych przez usługę Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).

### <a name="risk-events"></a>Zdarzenia ryzyka

Azure Active Directory korzysta z adaptacyjną uczenia algorytmów i heurystyki toodetect podejrzane akcji, które są tożsamości użytkownika powiązanych tooyour maszynowego. Witaj system tworzy rekord dla każdego wykrytego podejrzane działania. Te rekordy są także nazywane zdarzenia ryzyka.  
Aby uzyskać więcej informacji, zobacz [Zdarzenia o podwyższonym ryzyku w usłudze Azure Active Directory](active-directory-identity-protection-risk-events.md).


## <a name="investigation"></a>Badanie
Podróży za pomocą ochrony tożsamości zwykle zaczyna się od hello ochronę tożsamości z pulpitu nawigacyjnego.

![Korygowanie](./media/active-directory-identityprotection/1000.png "korygowania")

pulpit nawigacyjny Hello daje dostęp do:

* Raporty takie jak **użytkownicy oflagowani ryzyka**, **ryzyka zdarzenia** i **luk w zabezpieczeniach**
* Ustawienia, takie jak konfiguracja hello Twojej **zasady zabezpieczeń**, **powiadomienia** i **rejestracji usługi Multi-Factor authentication**

Zwykle to punkt startowy dochodzenia, które jest procesem hello sprawdzania hello działań, dzienniki i inne istotne informacje pokrewne tooa ryzyka toodecide zdarzeń czy korygowania lub migracji kroki są niezbędne, i jak został hello tożsamości uszkodzone i zrozumieć, jak hello naruszony tożsamości została użyta.

Można powiązać Twoje toohello działania dochodzenia [powiadomienia](active-directory-identityprotection-notifications.md) usługi Azure Active Directory Protection wysyła na wiadomości e-mail.

Witaj następujące sekcje zawierają bardziej szczegółowe informacje i hello kroki, które są powiązane tooan dochodzenia.  


## <a name="risky-sign-ins"></a>Ryzykowne logowania

Usługa Azure Active Directory wykryje [ryzyka typów zdarzeń](active-directory-reporting-risk-events.md#risk-event-types) w czasie rzeczywistym i w trybie offline. Każde zdarzenie zagrożenia wykrytego dla logowanie użytkownika wspiera tooa pojęcie logiczne o nazwie ryzykowne logowania. Ryzykowne logowanie jest wskaźnik prób logowania, które nie mogły zostać wykonane przez właściciela uzasadnionych hello konta użytkownika.


### <a name="sign-in-risk-level"></a>Poziom ryzyka logowania

Poziom ryzyka logowania jest wskazaniem (wysoki, średni lub niski) prawdopodobieństwo hello próba logowania nie została wykonana przez właściciela uzasadnionych hello konta użytkownika.

### <a name="mitigating-sign-in-risk-events"></a>Zmniejszenia zdarzenia logowania ryzyka

Środki zaradcze jest możliwość hello toolimit akcji tooexploit atakująca złamany tożsamości lub urządzenia bez przywracania hello tożsamości lub urządzenie tooa bezpieczne. Środki zaradcze nie można rozpoznać poprzednie zdarzenia logowania ryzyko związane z tożsamości hello lub urządzenia.

toomitigate ryzykowne logowania automatycznie, można skonfigurować policicies zabezpieczeń logowania ryzyka. Korzystając z tych zasad, należy wziąć pod uwagę poziom ryzyka hello hello użytkownika lub hello logowania tooblock ryzykowne logowania lub wymusić uwierzytelnianie wieloskładnikowe tooperform użytkownika hello. Te akcje mogą uniemożliwiać osobie atakującej wykorzystanie uszkodzenia toocause kradzieży tożsamości i może dać niektórych tożsamości hello toosecure czasu.

### <a name="sign-in-risk-security-policy"></a>Zasady zabezpieczeń logowania ryzyka
Zasady logowania ryzyko jest zasady dostępu warunkowego, która ocenia hello ryzyka tooa określonych logowania i stosuje środki zaradcze, na podstawie wstępnie zdefiniowane warunki i zasady.

![Zasady logowania ryzyka](./media/active-directory-identityprotection/1014.png "logowania zasad ryzyka")

Azure AD Identity Protection pomaga w zarządzaniu hello zmniejszenie ryzykowne logowania umożliwiając:

* Ustaw hello użytkowników i grup hello zasady ma zastosowanie do:

    ![Zasady logowania ryzyka](./media/active-directory-identityprotection/1015.png "logowania zasad ryzyka")
* Ustaw hello logowania ryzyka poziomu próg (niski, średni lub wysoki) wyzwalaną hello zasad:

    ![Zasady logowania ryzyka](./media/active-directory-identityprotection/1016.png "logowania zasad ryzyka")
* Toobe formanty hello zestaw wymuszane w przypadku wyzwala hello zasad:  

    ![Zasady logowania ryzyka](./media/active-directory-identityprotection/1017.png "logowania zasad ryzyka")
* Przełącz stan hello zasad:

    ![Rejestracja usługi MFA](./media/active-directory-identityprotection/403.png "rejestracji usługi MFA")
* Przegląd i ocena wpływu zmiany przed jej aktywowaniem hello:

    ![Zasady logowania ryzyka](./media/active-directory-identityprotection/1018.png "logowania zasad ryzyka")

#### <a name="what-you-need-tooknow"></a>Co należy tooknow
Można skonfigurować uwierzytelnianie wieloskładnikowe toorequire zasad logowania zagrożenia zabezpieczeń:

![Zasady logowania ryzyka](./media/active-directory-identityprotection/1017.png "logowania zasad ryzyka")

Jednak ze względu na bezpieczeństwo, to ustawienie działa tylko dla użytkowników, które zostały już zarejestrowane w usłudze Multi-Factor authentication. Jeśli uwierzytelnianie wieloskładnikowe toorequire warunku hello jest spełniony dla użytkownika, który nie jest jeszcze zarejestrowany w usłudze Multi-Factor authentication, użytkownik hello jest zablokowany.

Najlepszym rozwiązaniem Jeśli chcesz, aby uwierzytelnianie wieloskładnikowe toorequire ryzykowne logowania, wykonaj następujące czynności:

1. Włącz hello [zasady rejestracji usługi Multi-Factor authentication](#multi-factor-authentication-registration-policy) dla hello odpowiednich użytkowników.
2. Wymagaj hello wpływ na użytkowników toologin w tooperform-ryzykowne sesji rejestracji usługi MFA

Wykonanie tych kroków gwarantuje, że uwierzytelnianie wieloskładnikowe jest wymagany dla ryzykownych logowanie.

#### <a name="best-practices"></a>Najlepsze praktyki
Wybieranie **wysokiej** próg zmniejsza hello liczby zasad wyzwoleniu i minimalizuje hello toousers wpływu.  

Jednak nie obejmuje **małej** i **średni** logowania oznaczona flagą narażone na powitania zasad, które nie mogą blokować osoba atakująca możliwości wykorzystania złamany tożsamości.

Gdy ustawienie hello zasad,

* Wyklucz użytkowników, którzy nie / nie można wprowadzić uwierzytelnianie wieloskładnikowe
* Wyklucz użytkowników, których Włączanie hello zasad nie jest praktyczne ustawień regionalnych (na przykład nie toohelpdesk dostępu)
* Wyklucz użytkowników, którzy są prawdopodobnie toogenerate wiele alarmów false (deweloperów, analityków zabezpieczeń)
* Użyj **wysokiej** próg podczas początkowej zasad zbiorczego, lub jeśli należy zminimalizować problemy, które zostały odebrane przez użytkowników końcowych.
* Użyj **małej** progu, jeśli organizacja wymaga wyższego poziomu bezpieczeństwa. Wybieranie **małej** próg wprowadzono dodatkowe użytkownika logowania wyzwania, ale zwiększyć bezpieczeństwo.

Hello zalecane domyślne dla większości organizacji jest tooconfigure regułę **średni** toostrike próg kompromis między użyteczność i zabezpieczeń.

zasady logowania ryzyka Hello jest:

* Ruch przeglądarki tooall zastosowane i logowania korzystających z nowoczesnego uwierzytelniania.
* Nie zastosowano tooapplications przy użyciu starszych protokołów zabezpieczeń przez wyłączenie punktu końcowego usługi WS-Trust hello pod IDP hello federacyjne, takie jak usługi AD FS.

Witaj **zdarzenia o podwyższonym ryzyku** w konsoli Identity Protection hello zawiera listę wszystkich zdarzeń:

* Ta zasada została zastosowana do
* Można sprawdzić działanie hello i określenia, czy akcja hello się odpowiednie lub nie

Omówienie hello dotyczące środowiska użytkownika, zobacz:

* [Ryzykowne odzyskiwania logowania](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [Ryzykowne logowania zablokowane](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [Logowanie, korzystając z usługi Azure AD Identity Protection](active-directory-identityprotection-flows.md)  

**okno dialogowe konfiguracji pokrewne hello tooopen**:

- Na powitania **Azure AD Identity Protection** bloku w hello **Konfiguruj** kliknij **logowania zasad ryzyka**.

    ![Zasady użytkownika ridk](./media/active-directory-identityprotection/1014.png "zasady ridk użytkownika")



## <a name="users-flagged-for-risk"></a>Użytkownicy oflagowani w związku z ryzykiem

Wszystkie aktywne [ryzyka zdarzenia](active-directory-identity-protection-risk-events.md) zostały wykryte przez usługę Azure Active Directory dla użytkownika współtworzyć tooa pojęcie logiczne o nazwie użytkownika ryzyka. Użytkownik oznaczona flagą ryzyko jest wskaźnikiem dla konta użytkownika, który może być zagrożone.

![Użytkownicy oflagowani w związku z ryzykiem](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a>Poziom ryzyka użytkownika

Poziom ryzyka użytkownika będzie wskazywać (wysoki, średni lub niski) prawdopodobieństwo hello tożsamości użytkownika hello został złamany. Jego jest obliczany na podstawie zdarzeń hello ryzyka użytkownika, które są skojarzone z tożsamości użytkownika.

Witaj stan zdarzenia ryzyko jest **Active** lub **zamknięte**. Tylko ryzyka zdarzenia, które są **Active** współtworzenia obliczania poziomu ryzyka użytkownika toohello.

poziom ryzyka użytkownika Hello jest obliczana przy użyciu hello następujące dane wejściowe:

* Zdarzenia aktywne ryzyka wpływające na powitania użytkownika
* Poziom ryzyka tych zdarzeń
* Określa, czy wykonano wszystkie akcje naprawcze wykonane

![Ryzyko użytkownika](./media/active-directory-identityprotection/1031.png "zagrożeń użytkownika")

Użyj hello użytkownika ryzyka poziomy toocreate zasad dostępu warunkowego blokujące ryzykowne użytkownikom logowanie lub Wymuś je toosecurely zmienić swoje hasło.

### <a name="closing-risk-events-manually"></a>Zamknięcie zdarzenia o podwyższonym ryzyku ręcznie

W większości przypadków będzie wykonać akcje korygowania, takich jak zdarzenia Zamknij ryzyka tooautomatically resetowania hasła bezpiecznego. Jednak to może nie być możliwe.  
Dotyczy, na przykład Witaj, gdy:

* Użytkownik z zdarzenia Active ryzyka został usunięty.
* Badanie wykaże, że zdarzenie zagrożenia zgłoszony został wykonać przez wiarygodnego użytkownika hello

Ponieważ zdarzenia ryzyka, które są **Active** współtworzenia toohello użytkownika ryzyka obliczeń, może być toomanually obniżyć poziom ryzyka zamknięcie zdarzenia o podwyższonym ryzyku ręcznie.  
Podczas przebiegu hello dochodzenia można wybrać tootake żadnego z tych akcji toochange hello stan zdarzenia ryzyka:

![Akcje](./media/active-directory-identityprotection/34.png "akcje")

* **Rozwiąż** — Jeśli po zbadaniu zdarzenia ryzyka, trwało akcji korygowania odpowiednie poza ochrony tożsamości i uważasz, że zdarzenie ryzyka hello należy traktować jako zamknięte zdarzenie hello Oznacz jako rozwiązane. Zdarzenia rozwiązane ustawi tooClosed stan hello ryzyka zdarzeń i zdarzenia ryzyka hello przyczynia się już toouser ryzyka.
* **Oznacz jako fałszywie dodatnich** — w niektórych przypadkach można zbadać zdarzenia ryzyka i wykryć, czy został niepoprawnie oznaczone jako ryzykowne. Można ograniczyć liczbę hello takimi wystąpieniami przez oznaczenie zdarzeń ryzyka hello jako fałszywie dodatnich. Dzięki temu maszyny hello uczenia algorytmów tooimprove hello klasyfikacji podobnych zdarzeń w przyszłości hello. Stan Hello fałszywie dodatnich zdarzeń jest zbyt**zamknięte** i nie wpływają one toouser ryzyka.
* **Ignoruj** — Jeśli nie miały żadnych działań korygujących, ale mają hello usunięty z listy active hello toobe zdarzenia ryzyka, można oznaczyć zdarzeniem ryzyka Ignoruj i stan zdarzenia hello zostaną zamknięte. Zignorowano zdarzenia nie przyczyniają się toouser ryzyka. Tej opcji należy używać tylko w niezwykłych okolicznościach.
* **Uaktywnij ponownie** -ryzyka zdarzenia, które zostały ręcznie zamknięty (przez wybranie **rozwiązać**, **wynik fałszywie dodatni**, lub **Ignoruj**) można ponownie uaktywnić, ustawienie hello zdarzenia stanu z powrotem zbyt**Active**. Zdarzenia ponownie uaktywnione ryzyka współtworzenia obliczania poziomu ryzyka użytkownika toohello. Nie można ponownie uaktywnić zamknięte przy użyciu funkcji korygowania (takie jak resetowania hasła bezpiecznego) zdarzenia ryzyka.

**okno dialogowe konfiguracji pokrewne hello tooopen**:

1. Na powitania **Azure AD Identity Protection** bloku, w obszarze **zbadaj**, kliknij przycisk **ryzyka zdarzenia**.

    ![Resetowania hasła ręczne](./media/active-directory-identityprotection/1002.png "resetowania hasła ręczne")
2. W hello **ryzyka zdarzenia** kliknij zagrożenie.

    ![Resetowania hasła ręczne](./media/active-directory-identityprotection/1003.png "resetowania hasła ręczne")
3. W bloku ryzyka hello kliknij prawym przyciskiem myszy przez użytkownika.

    ![Resetowania hasła ręczne](./media/active-directory-identityprotection/1004.png "resetowania hasła ręczne")

### <a name="closing-all-risk-events-for-a-user-manually"></a>Ręczne zamknięcie wszystkich zdarzeń ryzyka dla użytkownika
Zamiast ręcznie indywidualnie zamknięcie zdarzenia ryzyka dla użytkownika, Azure Active Directory Identity Protection zapewnia także tooclose metody wszystkie zdarzenia dla użytkownika z jednego kliknięcia.

![Akcje](./media/active-directory-identityprotection/2222.png "akcje")

Po kliknięciu **odrzucić wszystkie zdarzenia**, wszystkie zdarzenia zostaną zamknięte i hello dotyczy użytkownika nie jest już na ryzyko.

### <a name="remediating-user-risk-events"></a>Zdarzenia o podwyższonym ryzyku korygując użytkownika

Korygowanie jest toosecure akcji tożsamości lub urządzeń, które wcześniej podejrzenia lub znane toobe naruszenia zabezpieczeń. Akcja korygowania przywraca hello tożsamości lub urządzenie tooa bezpieczne i usuwa poprzednie zdarzenia ryzyko związane z tożsamości hello lub urządzenia.

zdarzenia o podwyższonym ryzyku użytkownika tooremediate, można:

* Wykonaj ręcznie zdarzenia ryzyka bezpieczne hasło resetowania tooremediate użytkownika
* Konfigurowanie toomitigate zasad użytkownika zagrożenia zabezpieczeń lub automatycznie korygować zdarzenia o podwyższonym ryzyku użytkownika
* Ponowne instalowanie obrazu hello zainfekowanych urządzeń  

#### <a name="manual-secure-password-reset"></a>Resetowanie ręczne bezpiecznego hasła
Bezpieczne hasło jest skuteczne korygowania w przypadku wielu zdarzeń ryzyka i wykonywana, automatycznie powoduje zamknięcie zdarzenia o podwyższonym ryzyku i ponownie oblicza poziom ryzyka hello użytkownika. Możesz użyć hello Identity Protection pulpitu nawigacyjnego tooinitiate resetowania hasła dla użytkownika ryzykowne.

określone okno Hello zapewnia dwie różne metody tooreset hasła:

**Zresetuj hasło** — wybierz tę opcję **wymagają hasła hello użytkownika tooreset** tooallow hello odzyskiwania tooself użytkownika, jeśli użytkownik hello został zarejestrowany w usłudze Multi-Factor authentication. Podczas użytkownika hello następnym logowaniu użytkownik hello będzie toosolve wymagane uwierzytelnianie wieloskładnikowe pomyślnie testu i następnie, wymuszony toochange hello hasła. Ta opcja jest niedostępna, jeśli hello konto użytkownika nie jest już zarejestrowany uwierzytelnianie wieloskładnikowe.

**Hasło tymczasowe** — wybierz tę opcję **wygenerować hasło tymczasowe** tooimmediately unieważnienie hello istniejące hasło, a następnie utwórz nowe hasło tymczasowe hello użytkownika. Wyślij hello nowe hasło tymczasowe tooan alternatywny adres e-mail użytkownika hello lub Menedżera toohello użytkownika. Ponieważ hasło hello jest tymczasowy, użytkownik hello będzie toochange zostanie wyświetlony monit o hasło hello podawane podczas logowania.

![Zasady](./media/active-directory-identityprotection/1005.png "zasad")

**okno dialogowe konfiguracji pokrewne hello tooopen**:

1. Na powitania **Azure AD Identity Protection** bloku, kliknij przycisk **użytkownicy oflagowani ryzyka**.

    ![Resetowania hasła ręczne](./media/active-directory-identityprotection/1006.png "resetowania hasła ręczne")
2. Z listy hello użytkowników wybierz użytkownika z ryzyka co najmniej jednego zdarzenia.

    ![Resetowania hasła ręczne](./media/active-directory-identityprotection/1007.png "resetowania hasła ręczne")
3. W bloku użytkownika hello, kliknij **resetowania hasła**.

    ![Resetowania hasła ręczne](./media/active-directory-identityprotection/1008.png "resetowania hasła ręczne")

### <a name="user-risk-security-policy"></a>Zasady zabezpieczeń użytkownika ryzyka
Zasady zabezpieczeń użytkownika ryzyko jest zasady dostępu warunkowego, które ocenia hello ryzyka tooa poziomu określonego użytkownika, a następnie stosuje akcje korygowania i środki zaradcze, na podstawie wstępnie zdefiniowane warunki i zasady.

![Zasady użytkownika ridk](./media/active-directory-identityprotection/1009.png "zasady ridk użytkownika")

Azure AD Identity Protection pomaga w zarządzaniu łagodzenia hello i korygowania oflagowane ryzyka, umożliwiając użytkownikom:

* Ustaw hello użytkowników i grup hello zasady ma zastosowanie do:

    ![Zasady użytkownika ridk](./media/active-directory-identityprotection/1010.png "zasady ridk użytkownika")
* Ustaw hello użytkownika ryzyka poziomu próg (niski, średni lub wysoki) wyzwalaną hello zasad:

    ![Zasady użytkownika ridk](./media/active-directory-identityprotection/1011.png "zasady ridk użytkownika")
* Toobe formanty hello zestaw wymuszane w przypadku wyzwala hello zasad:

    ![Zasady użytkownika ridk](./media/active-directory-identityprotection/1012.png "zasady ridk użytkownika")
* Przełącz stan hello zasad:

    ![Zasady użytkownika ridk](./media/active-directory-identityprotection/403.png "rejestracji usługi MFA")
* Przegląd i ocena wpływu zmiany przed jej aktywowaniem hello:

    ![Zasady użytkownika ridk](./media/active-directory-identityprotection/1013.png "zasady ridk użytkownika")

Wybieranie **wysokiej** próg zmniejsza hello liczby zasad wyzwoleniu i minimalizuje hello toousers wpływu.
Jednak nie obejmuje **małej** i **średni** użytkowników oznaczona flagą narażone na powitania zasad, które mogą nie zapewnić tożsamości lub urządzenia, który zostały wcześniej podejrzanych lub znane toobe naruszenia zabezpieczeń.

Gdy ustawienie hello zasad,

* Wyklucz użytkowników, którzy są prawdopodobnie toogenerate wiele alarmów false (deweloperów, analityków zabezpieczeń)
* Wyklucz użytkowników, których Włączanie hello zasad nie jest praktyczne ustawień regionalnych (na przykład nie toohelpdesk dostępu)
* Użyj **wysokiej** próg podczas początkowej zasad zbiorczego, lub jeśli należy zminimalizować problemy, które zostały odebrane przez użytkowników końcowych.
* Użyj **małej** progu, jeśli organizacja wymaga wyższego poziomu bezpieczeństwa. Wybieranie **małej** próg wprowadzono dodatkowe użytkownika logowania wyzwania, ale zwiększyć bezpieczeństwo.

Hello zalecane domyślne dla większości organizacji jest tooconfigure regułę **średni** toostrike próg kompromis między użyteczność i zabezpieczeń.

Omówienie hello dotyczące środowiska użytkownika, zobacz:

* [Złamania zabezpieczeń konta przepływu odzyskiwania](active-directory-identityprotection-flows.md#compromised-account-recovery).  
* [Naruszone zablokowano konto przepływu](active-directory-identityprotection-flows.md#compromised-account-blocked).  

**okno dialogowe konfiguracji pokrewne hello tooopen**:

- Na powitania **Azure AD Identity Protection** bloku w hello **Konfiguruj** kliknij **zasad ryzyka użytkownika**.

    ![Zasady użytkownika ridk](./media/active-directory-identityprotection/1009.png "zasady ridk użytkownika")

### <a name="mitigating-user-risk-events"></a>Zmniejszenia zdarzenia o podwyższonym ryzyku użytkownika
Administratorzy mogą ustawić użytkowników tooblock zasad zabezpieczeń ryzyka użytkownika podczas logowania, w zależności od poziomu zagrożenia hello.

Blokowanie logowania:

* Uniemożliwia hello wygenerowanie nowego zdarzenia ryzyka użytkownika dla użytkownika hello, których to dotyczy
* Umożliwia administratorom toomanually Skoryguj hello ryzyka zdarzenia mające wpływ na tożsamości użytkownika hello i przywrócić stan bezpiecznego tooa



## <a name="multi-factor-authentication-registration-policy"></a>Zasady rejestracji usługi Multi-Factor authentication
Uwierzytelnianie wieloskładnikowe platformy Azure jest to metoda weryfikacji tożsamości, która wymaga stosowania hello więcej niż tylko nazwę użytkownika i hasło. Zapewnia drugą warstwę logowania toouser zabezpieczeń i transakcji.  
Firma Microsoft zaleca wymagane uwierzytelnianie wieloskładnikowe platformy Azure logowania użytkownika, ponieważ jego:

* Zapewnia silne uwierzytelnianie za pomocą różnych opcji weryfikacji łatwe
* Odgrywa kluczową rolę w celu przygotowania tooprotect Twojej organizacji i odzyskanie dokonywania konta

![Zasady użytkownika ridk](./media/active-directory-identityprotection/1019.png "zasady ridk użytkownika")

Aby uzyskać więcej informacji, zobacz [co to jest uwierzytelnianie wieloskładnikowe Azure?](../multi-factor-authentication/multi-factor-authentication.md)

Azure AD Identity Protection pomaga w zarządzaniu wdrożenie hello rejestracji usługi Multi-Factor authentication przez skonfigurowanie zasad, które umożliwia:

* Ustaw hello użytkowników i grup hello zasady ma zastosowanie do:

    ![Zasady MFA](./media/active-directory-identityprotection/1020.png "zasad MFA")
* Toobe formanty hello zestaw wymuszane w przypadku zasad hello wyzwala::  

    ![Zasady MFA](./media/active-directory-identityprotection/1021.png "zasad MFA")
* Przełącz stan hello zasad:

    ![Zasady MFA](./media/active-directory-identityprotection/403.png "zasad MFA")
* Wyświetl bieżący stan rejestracji hello:

    ![Zasady MFA](./media/active-directory-identityprotection/1022.png "zasad MFA")

Omówienie hello dotyczące środowiska użytkownika, zobacz:

* [Uwierzytelnianie wieloskładnikowe rejestracji przepływu](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).  
* [Logowanie napotyka przy użyciu usługi Azure AD Identity Protection](active-directory-identityprotection-flows.md).  

**okno dialogowe konfiguracji pokrewne hello tooopen**:

- Na powitania **Azure AD Identity Protection** bloku w hello **Konfiguruj** kliknij **rejestracji usługi Multi-Factor authentication**.

    ![Zasady MFA](./media/active-directory-identityprotection/1019.png "zasad MFA")

## <a name="next-steps"></a>Następne kroki
* [Kanał 9: Usługi Azure AD i Pokaż tożsamości: Podgląd ochrony tożsamości](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [Włączenie ochrony tożsamości usługi Azure Active Directory](active-directory-identityprotection-enable.md)

* [Luk w zabezpieczeniach wykrywanych przez usługę Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md)

* [Zdarzenia o podwyższonym ryzyku Azure Active Directory](active-directory-identity-protection-risk-events.md)

* [Azure Active Directory Identity Protection powiadomienia](active-directory-identityprotection-notifications.md)

* [Azure podręcznikowym ochronę tożsamości w usłudze Active Directory](active-directory-identityprotection-playbook.md)

* [Azure Active Directory Identity Protection słownik](active-directory-identityprotection-glossary.md)

* [Logowanie, korzystając z usługi Azure AD Identity Protection](active-directory-identityprotection-flows.md)

* [Azure Active Directory Identity Protection — jak toounblock użytkowników](active-directory-identityprotection-unblock-howto.md)

* [Wprowadzenie do usługi Azure Active Directory Identity Protection oraz Microsoft Graph](active-directory-identityprotection-graph-getting-started.md)
