---
title: 'Raportowanie: Azure AD SSPR | Dokumentacja firmy Microsoft'
description: "Raporty dotyczące usługi Azure AD samoobsługi hasła Resetowanie zdarzenia"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: af65b9be1e00c2819431694a5b0064b97b9e1867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-options-for-azure-ad-password-management"></a>Opcje raportowania dla usługi Azure AD zarządzania hasłami

Po wdrożeniu w wielu organizacjach przydatne tooknow jak lub jeśli SSPR naprawdę jest używany. Usługi Azure AD zapewnia funkcje raportowania, które ułatwiają pytania tooanswer przy użyciu puszkach raporty i jeśli są odpowiednio licencję, pozwalają toocreate zapytań niestandardowych.

Witaj następujące może odpowiedzieć na pytania przez raporty, które istnieją w hello [portalu Azure] (https://portal.azure.com/).

> [!NOTE]
> Musi być [administratora globalnego](active-directory-assign-admin-roles.md#assign-or-remove-administrator-roles) i może zdecydować się na dla to toobe danych zebranych w imieniu swojej organizacji przez zaproszonych hello raportowania tab lub inspekcji logowania co najmniej raz. Do tej czynności dane nie będą zbierane dla Twojej organizacji

* Ile osób zarejestrowano do resetowania hasła?
* Kto został zarejestrowany do resetowania hasła?
* Jakie dane osób rejestracji?
* Ile osób do resetowania haseł w hello ostatnich siedmiu dni
* Co to są hello najbardziej typowe metody użytkownicy lub Administratorzy tooreset swoje hasła?
* Jakie są typowe problemy krój użytkowników lub administratorów, podczas próby toouse resetowania hasła?
* Jakie Administratorzy są często Resetowanie własnych haseł?
* Czy istnieje wszelkich podejrzanych działań z przejściem z funkcją resetowania hasła?

## <a name="how-tooview-password-management-reports-in-hello-azure-portal"></a>Sposób zarządzania hasłami tooview raporty w programie hello portalu Azure

W hello obsługi portalu Azure zostały ulepszone sposób tooview resetowania i hasło rejestracji raport aktywności resetowania haseł.  Wykonaj kroki hello poniżej toofind hello hasła resetowania i hasło resetowania rejestracji zdarzeń:

1. Przejdź za[**portal.azure.com**](https://portal.azure.com)
2. Kliknij przycisk hello **więcej usług** menu na powitania głównego Azure po lewej stronie nawigacji w portalu
3. Wyszukaj **usługi Azure Active Directory** w hello listę usług i wybierz ją
4. Kliknij przycisk **użytkownicy i grupy** menu nawigacji hello Azure Active Directory
5. Kliknij przycisk hello **dzienników inspekcji** element nawigacji w menu nawigacji hello użytkownicy i grupy. To pokazuje wszystkie zdarzenia inspekcji hello wykonywane względem wszystkich użytkowników hello w katalogu. Można filtrować wszystkie hello hasła zdarzenia związane z, a także toosee tego widoku.
6. toofilter zdarzenia powiązane zresetować hasło hello tooonly widok, kliknij hello **filtru** u góry hello hello bloku.
7. Z hello **filtru** menu, wybierz hello **kategorii** listy rozwijanej i zmień je toohello **Samoobsługowe zarządzanie hasłami** typu kategorii.
8. Opcjonalnie dalsze listy hello filtrów przez wybranie określonych hello **działania** myślisz

## <a name="how-tooretrieve-password-management-events-from-hello-azure-ad-reports-and-events-api"></a>Jak tooretrieve hasło zarządzania zdarzenia z hello raportów usługi Azure AD i interfejsu API zdarzenia

Raporty Hello Azure AD i interfejsu API zdarzenia obsługuje wszystkie informacje hello w hasło resetowania hasła resetowania rejestracji raportów i pobierania. Przy użyciu tego interfejsu API, można pobrać resetowania hasła poszczególnych i resetowania hasła rejestrowania zdarzeń dla integracji z hello raportowania technologii wybranych przez użytkownika.

### <a name="how-tooget-started-with-hello-reporting-api"></a>Jak tooget pracę z interfejsem API raportowania hello

tooaccess te dane muszą toowrite małych aplikacji lub skryptu tooretrieve z naszych serwerów. [Dowiedz się, jak tooget wprowadzenie hello Azure AD interfejsu API raportowania](active-directory-reporting-api-getting-started.md).

Po utworzeniu skryptu pracy, następnie należy tooexamine hello hasła resetowania rejestracji zdarzeń i że można pobrać toomeet scenariuszy.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): Wyświetla kolumny hello dostępne dla zdarzeń resetowania hasła
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): Wyświetla listę dostępnych kolumn hello dla zdarzenia rejestracji resetowania hasła

### <a name="reporting-api-data-retrieval-limitations"></a>Ograniczenia pobierania danych interfejsu API raportowania

Obecnie hello raportów usługi Azure AD i interfejsu API zdarzenia pobiera się zbyt**75,000 pojedynczych zdarzeń** z hello [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) i [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) typów , obejmujących hello **ostatnich 30 dni**.

Jeśli konieczne tooretrieve lub przechowywania danych po przekroczeniu tego okna, zalecamy utrwalanie go w zewnętrznej bazy danych i przy użyciu hello interfejsu API tooquery hello delty, które powodują. Nasze zalecenie jest toobegin pobierania tych danych, gdy rozpocząć korzystanie z funkcji SSPR w Twojej organizacji, utrwalić go zewnętrznie, a następnie kontynuuj tootrack hello delty z tego punktu do przodu.

## <a name="how-toodownload-password-reset-registration-events-quickly-with-powershell"></a>Sposób hasła toodownload resetowania rejestracji zdarzeń szybko przy użyciu programu PowerShell

Ponadto toousing hello raportów usługi Azure AD i interfejsu API zdarzenia bezpośrednio, można także użyć hello poniżej zdarzenia rejestracji toorecent skrypt programu PowerShell w katalogu. Jest przydatne w przypadku, gdy chcesz toosee, który został ostatnio zarejestrowany lub chcesz tooensure, że wdrożenie resetowania hasła jest wykonywana zgodnie z oczekiwaniami.

* [Skrypt programu PowerShell działania rejestracji usługi Azure AD SSPR](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

### <a name="description-of-report-columns-in-azure-portal"></a>Opis kolumn raportu w portalu Azure

Witaj poniżej objaśniono kolumn raportu hello szczegółowo:

* **Użytkownik** — użytkownik hello, które próbowały hasła zresetować operacji rejestracji.
* **Rola** — Witaj rolę użytkownika hello w katalogu hello.
* **Data i godzina** — hello Data i godzina próby hello.
* **Dane zarejestrowane** — rejestracja resetowania podane podczas hasło użytkownika hello danych uwierzytelniania.

### <a name="description-of-report-values-in-azure-portal"></a>Opis raportu wartości w portalu Azure

Witaj poniższej tabeli opisano różne wartości hello dozwolone dla każdej kolumny:

| Kolumna | Dozwolone wartości i ich znaczenie |
| --- | --- |
| Data zarejestrowana |**Alternatywny adres E-mail** — użytkownik alternatywny adres e-mail lub uwierzytelniania wiadomości e-mail tooauthenticate<p><p>**Telefon biurowy**— office phone tooauthenticate używać użytkownika<p>**Telefon komórkowy** -tooauthenticate phone telefon komórkowy lub uwierzytelniania używać użytkownika<p>**Pytania zabezpieczające** — tooauthenticate pytania zabezpieczeń użytkownika używane<p>**Dowolną kombinację hello powyżej (np. alternatywny adres E-mail + telefon komórkowy)** — występuje, gdy zasady 2 bramy jest określona i pokazuje, które dwie metody hello tooauthentication użytkownika używany żądanie zresetowania hasła. |

## <a name="view-password-reset-activity-in-hello-classic-portal"></a>Aktywność w portalu klasycznym hello resetowania haseł widoku

Ten raport przedstawia resetowania hasła wszystkich prób, które wystąpiły w Twojej organizacji.

* **Maksymalny przedział czasu**: 30 dni
* **Maksymalna liczba wierszy**: 75 000
* **Do pobrania**: tak, przy użyciu pliku CSV

### <a name="description-of-report-columns-in-azure-classic-portal"></a>Opis kolumn raportu w klasycznym portalu Azure

Witaj poniżej objaśniono kolumn raportu hello szczegółowo:

1. **Użytkownik** — użytkownik hello, które próbowały hasła zresetować operacji (na podstawie hello identyfikator użytkownika pola pod warunkiem, gdy użytkownik hello tooreset hasła).
2. **Rola** — Witaj rolę użytkownika hello w katalogu hello.
3. **Data i godzina** — hello Data i godzina próby hello.
4. **Używane metody** — użytkownik hello metod uwierzytelniania to resetowania operacji.
5. **Wynik** — hello wynik hasła hello zresetować operacji.
6. **Szczegóły** — szczegóły hello Dlaczego resetowania hasła hello spowodowała wartość hello jak.  Zawiera również wszystkie kroki zaradcze może potrwać tooresolve wystąpił nieoczekiwany błąd.

### <a name="description-of-report-values-in-azure-classic-portal"></a>Opis wartości raportu w klasycznym portalu Azure

Witaj poniższej tabeli opisano różne wartości hello dozwolone dla każdej kolumny:

| Kolumna | Dozwolone wartości i ich znaczenie |
| --- | --- |
| Metody stosowane |**Alternatywny adres E-mail** — użytkownik alternatywny adres e-mail lub uwierzytelniania wiadomości e-mail tooauthenticate<p>**Telefon biurowy** — office phone tooauthenticate używać użytkownika<p>**Telefon komórkowy** — tooauthenticate phone telefon komórkowy lub uwierzytelniania używać użytkownika<p>**Pytania zabezpieczające** — tooauthenticate pytania zabezpieczeń użytkownika używane<p>**Dowolną kombinację hello powyżej (np. alternatywny adres E-mail + telefon komórkowy)** — występuje, gdy zasady 2 bramy jest określona i pokazuje, które dwie metody hello tooauthentication użytkownika używany żądanie zresetowania hasła. |
| wynik |**Porzucone** — użytkownika uruchomiony resetowania hasła, ale został zatrzymany połowie, za pośrednictwem, przerywając<p>**Zablokowane** — konto użytkownika zostało resetowania powodu stronę resetowania hasła hello toouse tooattempting hasła uniemożliwił toouse lub jednego hasła zresetować bramy zbyt wiele razy w okresie 24 godzin<p>**Anulowane** — uruchomiona resetowania hasła użytkownika, ale następnie kliknięto pozycję sesji hello toocancel hello przycisk Anuluj, które zostały części sposób za pomocą <p>**Skontaktować się z administratorem** — użytkownika wystąpił problem podczas jego sesji, które on nie można rozpoznać, więc hello użytkownik kliknął link "Skontaktuj się z administratorem" hello, zamiast Kończenie hasła hello resetowania przepływu<p>**Nie powiodło się** — użytkownik nie stanie tooreset hasła, prawdopodobnie ponieważ użytkownik hello nie został skonfigurowany toouse hello funkcji (na przykład nie licencji, brakujące informacje uwierzytelniania, hasło zarządzane lokalnego ale zapisywania zwrotnego jest wyłączone).<p>**Pomyślnie** — resetowania hasła zakończyło się pomyślnie. |
| Szczegóły |W poniższej tabeli w temacie |

### <a name="allowed-values-for-details-column"></a>Dozwolone wartości dla kolumny szczegółów

Poniżej znajduje się lista hello typów wyników, które mogą oczekiwać po przy użyciu hasła hello Zresetuj raport dotyczący działań:

| Szczegóły | Typ wyniku |
| --- | --- |
| Po zakończeniu opcji weryfikacji hello poczty e-mail użytkownika |porzucone |
| Po zakończeniu hello przenośnych opcji weryfikacji SMS użytkownika |porzucone |
| Po zakończeniu opcji weryfikacji wywołania przenośnych głosu hello użytkownika |porzucone |
| Po zakończeniu opcji weryfikacji wywołania hello office głosu użytkownika |porzucone |
| Po zakończeniu opcja pytania zabezpieczeń hello użytkownika |porzucone |
| Użytkownik porzucona po wprowadzeniu swój identyfikator użytkownika |porzucone |
| Porzucona po uruchomieniu opcji weryfikacji hello poczty e-mail użytkownika |porzucone |
| Porzucona po uruchomieniu opcji weryfikacji SMS hello mobilnych użytkownika |porzucone |
| Porzucona po uruchomieniu opcji weryfikacji wywołania przenośnych głosu hello użytkownika |porzucone |
| Porzucona po uruchomieniu opcji weryfikacji wywołania hello office głos użytkownika |porzucone |
| Porzucona po uruchomieniu opcji pytania zabezpieczeń hello użytkownika |porzucone |
| Porzucone przed wybraniem nowego hasła użytkownika |porzucone |
| Porzucone podczas wybierania nowego hasła użytkownika |porzucone |
| Użytkownik wprowadzono zbyt dużo nieprawidłowych kodów weryfikację SMS i jest zablokowany przez 24 godziny |Zablokowane |
| Użytkownik podjął próbę zbyt wiele prób weryfikacji głosu telefonu komórkowego i jest zablokowany przez 24 godziny |Zablokowane |
| Użytkownik podjął próbę office telefonu głosowej weryfikacji zbyt wiele razy i jest zablokowany przez 24 godziny |Zablokowane |
| Użytkownik podjął próbę pytania zabezpieczające tooanswer zbyt wiele razy i jest zablokowany przez 24 godziny |Zablokowane |
| Podjęto zbyt wiele razy tooverify numer telefonu użytkownika i jest zablokowany przez 24 godziny |Zablokowane |
| Użytkownik anulował przed przekazaniem hello wymagane metody uwierzytelniania |Anulowane |
| Użytkownik anulował przed przesłaniem nowe hasło |Anulowane |
| Użytkownik skontaktować się z administratorem po wypróbowaniu opcji weryfikacji hello poczty e-mail |Nawiązała kontakt z administratorem. |
| Użytkownik skontaktować się z administratorem po wypróbowaniu hello przenośnych opcji weryfikacji programu SMS |Nawiązała kontakt z administratorem. |
| Użytkownik skontaktować się z administratorem po wypróbowaniu opcji weryfikacji wywołania przenośnych głosu hello |Nawiązała kontakt z administratorem. |
| Użytkownik skontaktować się z administratorem po wypróbowaniu opcji weryfikacji wywołania hello office głosu |Nawiązała kontakt z administratorem. |
| Użytkownik skontaktować się z administratorem po wypróbowaniu opcji weryfikacji pytanie zabezpieczeń hello |Nawiązała kontakt z administratorem. |
| Resetowanie hasła nie jest włączona dla tego użytkownika. Resetowanie w obszarze hello hasła Włącz skonfigurować tooresolve kartę |Nie powiodło się |
| Użytkownik nie ma licencji. Tooresolve licencji toohello użytkownika można dodać to |Nie powiodło się |
| Użytkownik próbował tooreset z urządzenia bez plików cookie włączone |Nie powiodło się |
| Konto użytkownika ma niewystarczające uwierzytelniania metody zdefiniowane. Dodaj tooresolve informacje uwierzytelniania to |Nie powiodło się |
| Hasło użytkownika jest zarządzane lokalnie. Możesz je włączyć, tooresolve funkcji zapisywania zwrotnego haseł |Nie powiodło się |
| Nie można nawiązać połączenia lokalnej usługi resetowania hasła. Sprawdź dziennik zdarzeń na komputerze synchronizacji |Nie powiodło się |
| Wystąpił problem podczas resetowania hasła lokalne powitania użytkownika. Sprawdź dziennik zdarzeń na komputerze synchronizacji |Nie powiodło się |
| Ten użytkownik nie jest członkiem grupy Użytkownicy resetowania hasła hello. Dodaj tego użytkownika toothat grupy tooresolve to. |Nie powiodło się |
| Resetowanie hasła została wyłączona całkowicie dla tej dzierżawy. Zobacz [tutaj](http://aka.ms/ssprtroubleshoot) tooresolve to. |Nie powiodło się |
| Użytkownik pomyślnie zresetowano hasło |Powodzenie |

## <a name="self-service-password-management-activity-types"></a>Samoobsługowe zarządzanie hasłami typów działań

następujące typy działań Hello są wyświetlane w hello **Samoobsługowe zarządzanie hasłami** kategorii zdarzeń inspekcji.  Opis każdego z sposób.

* [**Zablokowano dostęp do samodzielnego resetowania hasła** ](#activity-type-blocked-from-self-service-password-reset) -wskazuje użytkownik podjął próbę tooreset hasła, użyj określonej bramy lub sprawdzić poprawności numeru telefonu więcej niż 5 razy całkowita w ciągu 24 godzin.
* [**Zmień hasło (internetowy)** ](#activity-type-change-password-self-service) — wskazuje użytkownika wykonywane dobrowolny lub wymusić (z powodu tooexpiry) zmiany hasła.
* [**Zresetuj hasło (Administrator)** ](#activity-type-reset-password-by-admin) — określa administrator wykonane resetowania w imieniu użytkownika z portalu Azure hello hasła.
* [**Zresetuj hasło (internetowy)** ](#activity-type-reset-password-self-service) -wskazuje użytkownik pomyślnie resetowania hasła z hello [Portal resetowania hasła programu Azure AD](https://passwordreset.microsoftonline.com).
* [**Samoobsługowego resetowania hasła postępu działań przepływu** ](#activity-type-self-serve-password-reset-flow-activity-progress) -wskazuje każdego kroku określonego użytkownika obejmującego (takich jak przekazywanie określonego hasła zresetować bramę uwierzytelniania), jako część hasła hello procesu resetowania.
* [**Odblokować konto użytkownika (internetowy)** ](#activity-type-unlock-user-account-self-service) -wskazuje użytkownik pomyślnie odblokowane swojego konta usługi Active Directory bez zresetowania hasła z hello [Portal resetowania hasła programu Azure AD](https://passwordreset.microsoftonline.com) przy użyciu Hello konta AD odblokowanie bez konieczności resetowania funkcji.
* [**Użytkownik jest zarejestrowany dla Samoobsługowe Resetowanie hasła** ](#activity-type-user-registered-for-self-service-password-reset) — wskazuje, użytkownik ma wszystkie wymagane hello informacji toobe stanie tooreset hasła zgodnie z hello obecnie określone zasady resetowania hasła dzierżawy.

### <a name="activity-type-blocked-from-self-service-password-reset"></a>Typ działania: zablokowano samoobsługowego resetowania hasła

następujące listy Hello wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje użytkownik podjął próbę tooreset hasła, użyj określonych bramy lub sprawdzania poprawności numeru telefonu więcej niż 5 razy całkowita w ciągu 24 godzin.
* **Działanie aktora** -hello użytkownika, który został ograniczony wykonywać dodatkowe operacje resetowania. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** -hello użytkownika, który został ograniczony wykonywać dodatkowe operacje resetowania. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
  * _Powodzenie_ -wskazuje użytkownika został ograniczony wykonywać żadnych dodatkowych resetuje, podejmować żadnych dodatkowych metod uwierzytelniania, albo do sprawdzania dodatkowych numerów hello następne 24 godziny.
* **Przyczyna niepowodzenia stanu działania** — nie dotyczy

### <a name="activity-type-change-password-self-service"></a>Typ działania: Zmień hasło (internetowy)

następujące listy Hello wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje użytkownika wykonywane dobrowolny lub wymusić (z powodu tooexpiry) zmiany hasła.
* **Działanie aktora** -hello użytkownika, który zmienił swoje hasło. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** -hello użytkownika, który zmienił swoje hasło. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
  * _Powodzenie_ -wskazuje użytkownik pomyślnie zmieniono hasło
  * _Błąd_ — wskazuje, użytkownik nie toochange swoje hasło. Kliknięcie przycisku Wiersz hello umożliwia toosee hello **przyczyny stanu działania** więcej informacji na temat przyczyny wystąpił błąd hello toolearn kategorii.
* **Przyczyna niepowodzenia stanu działania** - 
  * _FuzzyPolicyViolationInvalidPassword_ -hello użytkownik wybrał hasła, które zostało automatycznie zakazane powodu możliwości zakazane wykrywania hasła w tooMicrosoft znalezieniem toobe zbyt popularne lub szczególnie słabe.

### <a name="activity-type-reset-password-by-admin"></a>Typ działania: resetowania hasła (Administrator)

następujące listy Hello wyjaśniono tego działania szczegółowo:

* **Opis działania** — określa administrator wykonane resetowania w imieniu użytkownika z portalu Azure hello hasła.
* **Działanie aktora** -hello administratora, który wykonał hasła hello zresetować w imieniu innego użytkownika lub administratora. Musi być administratorem globalnym, hasło administratora, administrator użytkownika albo administratora pomocy technicznej.
* **Działania docelowego** -hello użytkownika, którego hasło zostało zresetowane. Może być użytkownika końcowego lub innego administratora.
* **Stany dozwolone działania**
  * _Powodzenie_ — wskazuje, jak administrator pomyślnie zresetowano hasło użytkownika
  * _Błąd_ — wskazuje, jak administrator nie toochange hasła użytkownika. Kliknięcie przycisku Wiersz hello umożliwia toosee hello **przyczyny stanu działania** więcej informacji na temat przyczyny wystąpił błąd hello toolearn kategorii.

### <a name="activity-type-reset-password-self-service"></a>Typ działania: resetowania hasła (internetowy)

następujące listy Hello wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje użytkownik pomyślnie resetowania hasła z hello [Portal resetowania hasła programu Azure AD](https://passwordreset.microsoftonline.com).
* **Działanie aktora** — użytkownik hello resetowania hasła. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** — użytkownik hello resetowania hasła. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
  * _Powodzenie_ -wskazuje użytkownik pomyślnie resetować swoje hasła
  * _Błąd_ — wskazuje, użytkownik nie tooreset swoje hasła. Kliknięcie przycisku Wiersz hello umożliwia toosee hello **przyczyny stanu działania** więcej informacji na temat przyczyny wystąpił błąd hello toolearn kategorii.
* **Przyczyna niepowodzenia stanu działania** -
  * _FuzzyPolicyViolationInvalidPassword_ — Witaj, Administratorze wybrane hasła, które zostało automatycznie zakazane powodu możliwości zakazane wykrywania hasła w tooMicrosoft znalezieniem toobe zbyt popularne lub szczególnie słabe.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>Typ działania: Self służyć postępu działań przepływu resetowania hasła

następujące listy Hello wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje każdego kroku określonego użytkownika obejmującego (takich jak przekazywanie określonego hasła zresetować bramę uwierzytelniania) jako część hasła hello procesu resetowania.
* **Działanie aktora** -hello użytkownika, który wykonał część hasła hello zresetować przepływu. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** -hello użytkownika, który wykonał część hasła hello zresetować przepływu. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
  * _Powodzenie_ -wskazuje użytkownika zostało pomyślnie ukończone określonego kroku przepływu resetowania hasła hello.
  * _Błąd_ -wskazuje określonego kroku hasła hello resetować przepływu nie powiodło się. Kliknięcie przycisku Wiersz hello umożliwia toosee hello **przyczyny stanu działania** więcej informacji na temat przyczyny wystąpił błąd hello toolearn kategorii.
* **Dozwolone przyczyny stanu działania**
  * Zobacz tabelę poniżej, aby [wszystkie dozwolone aktywności resetowania przyczyny stanu](#allowed-values-for-details-column)

### <a name="activity-type-unlock-user-account-self-service"></a>Typ działania: odblokować konto użytkownika (internetowy)

następujące listy Hello wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje użytkownik pomyślnie odblokowane swojego konta usługi Active Directory bez zresetowania hasła z hello [Portal resetowania hasła programu Azure AD](https://passwordreset.microsoftonline.com) przy użyciu konta hello AD odblokowanie bez konieczności resetowania Funkcja.
* **Działanie aktora** — użytkownik hello odblokowane ich kont bez zresetowania hasła. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** — użytkownik hello odblokowane ich kont bez zresetowania hasła. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
  * _Powodzenie_ -wskazuje użytkownik pomyślnie odblokowane własne konto
  * _Błąd_ — wskazuje, użytkownik nie toounlock swojego konta. Kliknięcie przycisku Wiersz hello umożliwia toosee hello **przyczyny stanu działania** więcej informacji na temat przyczyny wystąpił błąd hello toolearn kategorii.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Typ działania: użytkownik jest zarejestrowany dla samoobsługowego resetowania hasła

następujące listy Hello wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje, użytkownik ma wszystkie wymagane hello informacji toobe stanie tooreset hasła zgodnie z hello obecnie określone zasady resetowania hasła dzierżawy. 
* **Działanie aktora** -hello użytkownik zarejestrowany w celu resetowania haseł. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** -hello użytkownik zarejestrowany w celu resetowania haseł. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
  * _Powodzenie_ -wskazuje pomyślnie zarejestrowany do resetowania zgodnie z zasadami bieżącego hello hasła użytkownika. 
  * _Błąd_ -wskazuje tooregister użytkownika nie powiodło się, w celu resetowania haseł. Kliknięcie przycisku Wiersz hello umożliwia toosee hello **przyczyny stanu działania** więcej informacji na temat przyczyny wystąpił błąd hello toolearn kategorii. Uwaga - oznacza to użytkownik jest tooreset swoje hasła, po prostu, że nie zakończyła hello procesu rejestracji. Jeśli niezweryfikowane dane na koncie jest prawidłowa (takich jak numer telefonu, który nie jest sprawdzana poprawność), nawet jeśli ich nie została zweryfikowana ten numer telefonu, mogą nadal go używać tooreset swoje hasło. Aby uzyskać więcej informacji, zobacz [co się dzieje, gdy użytkownik rejestruje?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="next-steps"></a>Następne kroki

Witaj następującego łącza znajdują się dodatkowe informacje dotyczące resetowania przy użyciu usługi Azure AD

* [Dzienniki inspekcji zarządzania toouser skrótów](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit) — przejdź bezpośrednio dzienniki inspekcji dzierżawy tooyour Zarządzanie użytkownikami
* [**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD 
* [**Licencjonowanie**](active-directory-passwords-licensing.md) — Konfigurowanie licencjonowania w usłudze Azure AD
* [**Dane** ](active-directory-passwords-data.md) — zrozumieć dane hello jest wymagany i jak służy do zarządzania hasłami
* [**Wdrożenie** ](active-directory-passwords-best-practices.md) — planowanie i wdrażanie SSPR tooyour użytkowników przy użyciu wskazówek hello znaleźć tutaj
* [**Dostosowywanie** ](active-directory-passwords-customize.md) — Dostosowywanie hello wygląd i działanie hello SSPR środowisko firmy.
* [**Nowości techniczne** ](active-directory-passwords-how-it-works.md) -przejdź za hello ściany toounderstand, jak to działa
* [**Często zadawane pytania**](active-directory-passwords-faq.md) — Jak? Dlaczego? Co? Gdzie? Kto? Kiedy? -Tooquestions tooask chciał zawsze odpowiada
* [**Rozwiązywanie problemów z** ](active-directory-passwords-troubleshoot.md) — Dowiedz się, jak tooresolve typowe problemy, widzimy z SSPR
* [**Zasady**](active-directory-passwords-policy.md) — Omówienie zasad haseł usługi Azure AD i ich ustawianie
