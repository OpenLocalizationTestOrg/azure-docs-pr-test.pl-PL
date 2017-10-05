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
ms.openlocfilehash: ba7b36e654aa0bf3b74d42a2b0ae96ae2a9b6241
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-options-for-azure-ad-password-management"></a>Opcje raportowania dla usługi Azure AD zarządzania hasłami

Po wdrożeniu w wielu organizacjach chcieli wiedzieć, jak lub jeśli SSPR jest rzeczywiście używane. Usługa Azure AD zapewnia funkcje raportowania, które ułatwiają odpowiedzi na pytania przy użyciu zwięzłych raportów i czy masz odpowiednio licencję, pozwala na tworzenie zapytań niestandardowych.

Może być odpowiedzieć na następujące pytania przez raporty, które istnieją w [portalu Azure] (https://portal.azure.com/).

> [!NOTE]
> Musi być [administratora globalnego](active-directory-assign-admin-roles.md#assign-or-remove-administrator-roles) i może zdecydować się na tych danych do zebrania imieniu swojej organizacji, odwiedzając raportowania dzienniki tab lub inspekcji, co najmniej raz. Do tej czynności dane nie będą zbierane dla Twojej organizacji

* Ile osób zarejestrowano do resetowania hasła?
* Kto został zarejestrowany do resetowania hasła?
* Jakie dane osób rejestracji?
* Ile osób do resetowania hasła w ciągu ostatnich siedmiu dni
* Co to są najbardziej typowe metody użytkowników lub administratorów za pomocą resetowanie haseł?
* Jakie są typowe problemy użytkownicy lub Administratorzy krój podczas próby użycia resetowania hasła?
* Jakie Administratorzy są często Resetowanie własnych haseł?
* Czy istnieje wszelkich podejrzanych działań z przejściem z funkcją resetowania hasła?

## <a name="how-to-view-password-management-reports-in-the-azure-portal"></a>Jak wyświetlić raporty zarządzania hasło w portalu Azure

W portalu Azure doświadczenia mamy ulepszone sposobem wyświetlenia resetowania hasła i rejestracji aktywność resetowania haseł.  Wykonaj poniższe kroki, aby znaleźć resetowania resetowania hasła i hasło rejestracji zdarzeń:

1. Przejdź do [ **portal.azure.com**](https://portal.azure.com)
2. Kliknij przycisk **więcej usług** menu głównego Azure nawigacji po lewej stronie portalu
3. Wyszukaj **usługi Azure Active Directory** na liście usług i wybierz ją
4. Kliknij przycisk **użytkownicy i grupy** w menu nawigacyjnym usługi Azure Active Directory
5. Kliknij przycisk **dzienników inspekcji** element nawigacji w menu nawigacyjnym użytkownicy i grupy. To pokazuje wszystkie zdarzenia inspekcji występujące przeciwko wszyscy użytkownicy w katalogu. Ten widok, aby wyświetlić wszystkie powiązane hasło zdarzenia, a także można filtrować.
6. Aby filtrować tego widoku i tylko zdarzenia powiązane resetowania hasła, kliknij przycisk **filtru** u góry bloku.
7. Z **filtru** menu, wybierz opcję **kategorii** listy rozwijanej i zmień go na **Samoobsługowe zarządzanie hasłami** typu kategorii.
8. Opcjonalnie dalsze Filtruj listę, wybierając konkretnym **działania** myślisz

## <a name="how-to-retrieve-password-management-events-from-the-azure-ad-reports-and-events-api"></a>Jak pobrać hasło zdarzeń zarządzania raportów usługi Azure AD i interfejsu API zdarzenia

Raportów usługi Azure AD i interfejsu API zdarzenia obsługuje wszystkie informacje zawarte w hasło resetowania hasła resetowania rejestracji raportów i pobierania. Przy użyciu tego interfejsu API, można pobrać resetowania hasła poszczególnych i rejestracji zdarzeń do integracji z technologii raportowania wybranym resetowania hasła.

### <a name="how-to-get-started-with-the-reporting-api"></a>Jak rozpocząć pracę z interfejsem API raportowania

Aby uzyskać dostęp do tych danych, należy napisać małych aplikacji lub skrypt, aby pobrać go ze swoich serwerów. [Dowiedz się, jak rozpocząć pracę z usługi Azure AD API raportowania](active-directory-reporting-api-getting-started.md).

Po utworzeniu skryptu pracy, następnie należy zbadać hasła resetowania i rejestracji zdarzenia, które można pobrać, aby spełnić scenariuszy.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): Wyświetla listę dostępnych kolumn zdarzeń resetowania hasła
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): Wyświetla listę dostępnych kolumn dla zdarzenia rejestracji resetowania hasła

### <a name="reporting-api-data-retrieval-limitations"></a>Ograniczenia pobierania danych interfejsu API raportowania

Obecnie raportów usługi Azure AD i interfejsu API zdarzenia pobiera do **75,000 pojedynczych zdarzeń** z [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) i [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) typów Łączenie węzłów **ostatnich 30 dni**.

Jeśli potrzebujesz do pobierania lub przechowywania danych po przekroczeniu tego okna, zalecamy utrwalanie go w zewnętrznej bazy danych i do badania delty, które powodują przy użyciu interfejsu API. Jest nasze zalecenie, aby rozpocząć pobieranie tych danych podczas uruchamiania w organizacji za pomocą funkcji SSPR, utrwalić go zewnętrznie, a następnie przejdź do śledzenia może od tego momentu.

## <a name="how-to-download-password-reset-registration-events-quickly-with-powershell"></a>Jak pobrać zdarzenia rejestracji resetowania haseł szybko przy użyciu programu PowerShell

Oprócz bezpośrednio za pomocą raportów usługi Azure AD i interfejsu API zdarzenia, można także użyć poniższego skryptu programu PowerShell, aby ostatnie zdarzenia rejestracji w katalogu. Jest to przydatne w przypadku, gdy użytkownik chce zobaczyć, kto został ostatnio zarejestrowany lub chcesz upewnij się, że wdrożenia resetowania hasła jest wykonywana zgodnie z oczekiwaniami.

* [Skrypt programu PowerShell działania rejestracji usługi Azure AD SSPR](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

### <a name="description-of-report-columns-in-azure-portal"></a>Opis kolumn raportu w portalu Azure

Poniżej objaśniono szczegółowo kolumn raportu:

* **Użytkownik** — operacja rejestracji zresetować użytkownika, które próbowały hasła.
* **Rola** — rola użytkownika w katalogu.
* **Data i godzina** — Data i godzina próby.
* **Dane zarejestrowane** — jakie dane uwierzytelniania użytkownika podana podczas hasło rejestracji resetowania.

### <a name="description-of-report-values-in-azure-portal"></a>Opis raportu wartości w portalu Azure

W poniższej tabeli opisano różne wartości dla każdej kolumny:

| Kolumna | Dozwolone wartości i ich znaczenie |
| --- | --- |
| Data zarejestrowana |**Alternatywny adres E-mail** — użytkownika używany alternatywny adres e-mail lub uwierzytelniania wiadomości e-mail do uwierzytelniania<p><p>**Telefon biurowy**— telefon biurowy użytkownika służące do uwierzytelniania<p>**Telefon komórkowy** — użytkownik telefon komórkowy lub numer telefonu uwierzytelniania do uwierzytelniania<p>**Pytania zabezpieczające** — używane przez użytkownika pytań zabezpieczających do uwierzytelniania<p>**Dowolną kombinację powyżej (np. alternatywny adres E-mail + telefon komórkowy)** — występuje, gdy zasady 2 bramy jest określona i przedstawia które dwie metody użytkownika służące do uwierzytelniania żądanie zresetowania hasła. |

## <a name="view-password-reset-activity-in-the-classic-portal"></a>Aktywność w klasycznym portalu resetowania haseł widoku

Ten raport przedstawia resetowania hasła wszystkich prób, które wystąpiły w Twojej organizacji.

* **Maksymalny przedział czasu**: 30 dni
* **Maksymalna liczba wierszy**: 75 000
* **Do pobrania**: tak, przy użyciu pliku CSV

### <a name="description-of-report-columns-in-azure-classic-portal"></a>Opis kolumn raportu w klasycznym portalu Azure

Poniżej objaśniono szczegółowo kolumn raportu:

1. **Użytkownik** — użytkownik, które próbowały hasła zresetować operacji (na podstawie Identyfikatora użytkownika pola pod warunkiem, gdy użytkownik jest dostarczany do resetowania hasła).
2. **Rola** — rola użytkownika w katalogu.
3. **Data i godzina** — Data i godzina próby.
4. **Używane metody** — metod uwierzytelniania użytkownika używane przez ten zresetować operacji.
5. **Wynik** — operacji resetowania wynik hasło.
6. **Szczegóły** — szczegóły Dlaczego zresetować hasła spowodowała jak wartość.  Obejmuje też kroki wszelkie środki zaradcze, może potrwać do rozpoznania wystąpił nieoczekiwany błąd.

### <a name="description-of-report-values-in-azure-classic-portal"></a>Opis wartości raportu w klasycznym portalu Azure

W poniższej tabeli opisano różne wartości dla każdej kolumny:

| Kolumna | Dozwolone wartości i ich znaczenie |
| --- | --- |
| Metody stosowane |**Alternatywny adres E-mail** — użytkownika używany alternatywny adres e-mail lub uwierzytelniania wiadomości e-mail do uwierzytelniania<p>**Telefon biurowy** — telefon biurowy użytkownika służące do uwierzytelniania<p>**Telefon komórkowy** — użytkownik telefon komórkowy lub numer telefonu uwierzytelniania do uwierzytelniania<p>**Pytania zabezpieczające** — używane przez użytkownika pytań zabezpieczających do uwierzytelniania<p>**Dowolną kombinację powyżej (np. alternatywny adres E-mail + telefon komórkowy)** — występuje, gdy zasady 2 bramy jest określona i przedstawia które dwie metody użytkownika służące do uwierzytelniania żądanie zresetowania hasła. |
| wynik |**Porzucone** — użytkownika uruchomiony resetowania hasła, ale został zatrzymany połowie, za pośrednictwem, przerywając<p>**Zablokowane** — konto użytkownika nie mógł używać resetowania z powodu próby hasła do strony resetowania hasła lub jednego hasła zresetować bramy zbyt wiele razy w okresie 24 godzin<p>**Anulowane** — uruchomiona resetowania hasła użytkownika, ale następnie kliknięto przycisk Anuluj, aby anulować części sposób za pomocą sesji <p>**Skontaktować się z administratorem** — użytkownika wystąpił problem podczas jego sesji, które on nie można rozpoznać, więc użytkownik kliknął link "Skontaktuj się z administratorem" zamiast zakończenie przepływu zresetować hasła<p>**Nie powiodło się** — użytkownik nie mógł zresetować hasło, prawdopodobnie ponieważ użytkownik nie został skonfigurowany do używania funkcji (na przykład nie licencji, brakujące informacje uwierzytelniania, hasło zarządzane lokalnego ale zapisywania zwrotnego jest wyłączone).<p>**Pomyślnie** — resetowania hasła zakończyło się pomyślnie. |
| Szczegóły |W poniższej tabeli w temacie |

### <a name="allowed-values-for-details-column"></a>Dozwolone wartości dla kolumny szczegółów

Poniżej przedstawiono listę typów wyników, które mogą oczekiwać po przy użyciu hasła Zresetuj raport dotyczący działań:

| Szczegóły | Typ wyniku |
| --- | --- |
| Po zakończeniu opcja weryfikacji wiadomości e-mail użytkownika |porzucone |
| Po zakończeniu przenośnych opcji weryfikacji SMS użytkownika |porzucone |
| Po zakończeniu opcji weryfikacji wywołania przenośnych głosu użytkownika |porzucone |
| Po zakończeniu opcję weryfikacji połączenia głosowe office użytkownika |porzucone |
| Przerwane po zakończeniu zabezpieczeń pytania opcji użytkownika |porzucone |
| Użytkownik porzucona po wprowadzeniu swój identyfikator użytkownika |porzucone |
| Porzucona po uruchomieniu opcji weryfikacji poczty e-mail użytkownika |porzucone |
| Użytkownik porzucona po uruchomieniu opcji mobilnych weryfikację SMS |porzucone |
| Porzucona po uruchomieniu opcji weryfikacji wywołania przenośnych głos użytkownika |porzucone |
| Użytkownik porzucona po uruchomieniu opcji weryfikacji wywołania głosu pakietu office |porzucone |
| Przerwane po uruchamianie zabezpieczeń pytania opcji użytkownika |porzucone |
| Porzucone przed wybraniem nowego hasła użytkownika |porzucone |
| Porzucone podczas wybierania nowego hasła użytkownika |porzucone |
| Użytkownik wprowadzono zbyt dużo nieprawidłowych kodów weryfikację SMS i jest zablokowany przez 24 godziny |Zablokowane |
| Użytkownik podjął próbę zbyt wiele prób weryfikacji głosu telefonu komórkowego i jest zablokowany przez 24 godziny |Zablokowane |
| Użytkownik podjął próbę office telefonu głosowej weryfikacji zbyt wiele razy i jest zablokowany przez 24 godziny |Zablokowane |
| Użytkownik próbował odpowiedzi na pytania zabezpieczające zbyt wiele prób i jest zablokowany przez 24 godziny |Zablokowane |
| Użytkownik próbował Sprawdź numer telefonu zbyt wiele prób i jest zablokowany przez 24 godziny |Zablokowane |
| Użytkownik anulował przed przekazaniem ich z metod uwierzytelniania |Anulowane |
| Użytkownik anulował przed przesłaniem nowe hasło |Anulowane |
| Użytkownik skontaktować się z administratorem po wypróbowaniu opcja weryfikacji wiadomości e-mail |Nawiązała kontakt z administratorem. |
| Użytkownik skontaktować się z administratorem po wypróbowaniu przenośnych opcji weryfikacji programu SMS |Nawiązała kontakt z administratorem. |
| Użytkownik skontaktować się z administratorem po wypróbowaniu opcji weryfikacji wywołania przenośnych głosu |Nawiązała kontakt z administratorem. |
| Użytkownik skontaktować się z administratorem po wypróbowaniu opcję weryfikacji połączenia głosowe pakietu office |Nawiązała kontakt z administratorem. |
| Użytkownik skontaktować się z administratorem po wypróbowaniu opcji weryfikacji pytanie zabezpieczeń |Nawiązała kontakt z administratorem. |
| Resetowanie hasła nie jest włączona dla tego użytkownika. Włącz resetowania na karcie Konfiguracja, aby rozwiązać ten problem |Nie powiodło się |
| Użytkownik nie ma licencji. Możesz dodać licencję do użytkownika, aby rozwiązać ten problem |Nie powiodło się |
| Użytkownik próbował zresetować z urządzenia bez plików cookie włączone |Nie powiodło się |
| Konto użytkownika ma niewystarczające uwierzytelniania metody zdefiniowane. Dodaj informacje uwierzytelniania, aby rozwiązać ten problem |Nie powiodło się |
| Hasło użytkownika jest zarządzane lokalnie. Można włączyć funkcję zapisywania zwrotnego haseł rozwiązać ten problem |Nie powiodło się |
| Nie można nawiązać połączenia lokalnej usługi resetowania hasła. Sprawdź dziennik zdarzeń na komputerze synchronizacji |Nie powiodło się |
| Wystąpił problem podczas resetowania użytkownika lokalnego hasła. Sprawdź dziennik zdarzeń na komputerze synchronizacji |Nie powiodło się |
| Ten użytkownik nie jest członkiem grupy Użytkownicy resetowania hasła. Dodaj tego użytkownika do tej grupy, aby rozwiązać ten problem. |Nie powiodło się |
| Resetowanie hasła została wyłączona całkowicie dla tej dzierżawy. Zobacz [tutaj](http://aka.ms/ssprtroubleshoot) Aby rozwiązać ten problem. |Nie powiodło się |
| Użytkownik pomyślnie zresetowano hasło |Powodzenie |

## <a name="self-service-password-management-activity-types"></a>Samoobsługowe zarządzanie hasłami typów działań

Następujące typy działań są wyświetlane w **Samoobsługowe zarządzanie hasłami** kategorii zdarzeń inspekcji.  Opis każdego z sposób.

* [**Zablokowano dostęp do samodzielnego resetowania hasła** ](#activity-type-blocked-from-self-service-password-reset) -wskazuje użytkownik próbował zresetować hasło, użyj określonych bramy lub sprawdzania poprawności numeru telefonu więcej niż 5 razy całkowita w ciągu 24 godzin.
* [**Zmień hasło (internetowy)** ](#activity-type-change-password-self-service) -wskazuje użytkownika wykonywane dobrowolny lub wymusić (z powodu wygaśnięcia) zmiany hasła.
* [**Zresetuj hasło (Administrator)** ](#activity-type-reset-password-by-admin) — określa administrator wykonane resetowania w imieniu użytkownika z portalu Azure hasła.
* [**Zresetuj hasło (internetowy)** ](#activity-type-reset-password-self-service) -wskazuje użytkownik pomyślnie resetowania hasła z [Portal resetowania hasła programu Azure AD](https://passwordreset.microsoftonline.com).
* [**Samoobsługowego resetowania hasła postępu działań przepływu** ](#activity-type-self-serve-password-reset-flow-activity-progress) -wskazuje każdego kroku określonego użytkownika obejmującego (takich jak przekazywanie określonego hasła zresetować bramę uwierzytelniania), jako część hasło procesu resetowania.
* [**Odblokować konto użytkownika (internetowy)** ](#activity-type-unlock-user-account-self-service) -wskazuje użytkownik pomyślnie odblokowane swojego konta usługi Active Directory bez zresetowania hasła z [Portal resetowania hasła programu Azure AD](https://passwordreset.microsoftonline.com) przy użyciu usługi AD bez funkcji resetowania odblokowania konta.
* [**Użytkownik jest zarejestrowany dla Samoobsługowe Resetowanie hasła** ](#activity-type-user-registered-for-self-service-password-reset) — wskazuje, użytkownik ma wszystkie wymagane informacje, aby można było do zresetowania swojego hasła zgodnie z obecnie określonego dzierżawcę zasady resetowania hasła.

### <a name="activity-type-blocked-from-self-service-password-reset"></a>Typ działania: zablokowano samoobsługowego resetowania hasła

Poniżej wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje użytkownik próbował zresetować hasło, użyj określonych bramy lub sprawdzania poprawności numeru telefonu więcej niż 5 razy całkowita w ciągu 24 godzin.
* **Działanie aktora** — użytkownik, który został ograniczony wykonywać dodatkowe operacje resetowania. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** — użytkownik, który został ograniczony wykonywać dodatkowe operacje resetowania. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
  * _Powodzenie_ -wskazuje użytkownika został ograniczony wykonywać żadnych dodatkowych resetuje, podejmować żadnych dodatkowych metod uwierzytelniania, albo do sprawdzania żadnych dodatkowych numerów telefonów przez następne 24 godziny.
* **Przyczyna niepowodzenia stanu działania** — nie dotyczy

### <a name="activity-type-change-password-self-service"></a>Typ działania: Zmień hasło (internetowy)

Poniżej wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje użytkownika wykonywane dobrowolny lub wymusić (z powodu wygaśnięcia) zmiany hasła.
* **Działanie aktora** -użytkownika, który zmienił swoje hasło. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** -użytkownika, który zmienił swoje hasło. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
  * _Powodzenie_ -wskazuje użytkownik pomyślnie zmieniono hasło
  * _Błąd_ -wskazuje użytkownika nie można zmienić swoje hasło. Kliknięcie przycisku wiersz umożliwia zobacz **przyczyny stanu działania** kategorię, aby dowiedzieć się więcej na temat przyczyny błędu.
* **Przyczyna niepowodzenia stanu działania** - 
  * _FuzzyPolicyViolationInvalidPassword_ — użytkownik wybrał hasła, które zostało automatycznie zakazane dzięki możliwościom zakazane wykrywania hasła firmy Microsoft znalezieniem zbyt popularne lub szczególnie słabe.

### <a name="activity-type-reset-password-by-admin"></a>Typ działania: resetowania hasła (Administrator)

Poniżej wyjaśniono tego działania szczegółowo:

* **Opis działania** — określa administrator wykonane resetowania w imieniu użytkownika z portalu Azure hasła.
* **Działanie aktora** -administratora, który wykonał resetowania w imieniu innego użytkownika lub administratora hasła. Musi być administratorem globalnym, hasło administratora, administrator użytkownika albo administratora pomocy technicznej.
* **Działania docelowego** -użytkownika, którego hasło zostało zresetowane. Może być użytkownika końcowego lub innego administratora.
* **Stany dozwolone działania**
  * _Powodzenie_ — wskazuje, jak administrator pomyślnie zresetowano hasło użytkownika
  * _Błąd_ — wskazuje, jak administrator nie można zmienić hasła użytkownika. Kliknięcie przycisku wiersz umożliwia zobacz **przyczyny stanu działania** kategorię, aby dowiedzieć się więcej na temat przyczyny błędu.

### <a name="activity-type-reset-password-self-service"></a>Typ działania: resetowania hasła (internetowy)

Poniżej wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje użytkownik pomyślnie resetowania hasła z [Portal resetowania hasła programu Azure AD](https://passwordreset.microsoftonline.com).
* **Działanie aktora** — użytkownik, który resetowania hasła. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** — użytkownik, który resetowania hasła. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
  * _Powodzenie_ -wskazuje użytkownik pomyślnie resetować swoje hasła
  * _Błąd_ — wskazuje, nie można zresetować swoje hasła użytkownika. Kliknięcie przycisku wiersz umożliwia zobacz **przyczyny stanu działania** kategorię, aby dowiedzieć się więcej na temat przyczyny błędu.
* **Przyczyna niepowodzenia stanu działania** -
  * _FuzzyPolicyViolationInvalidPassword_ — administrator wybrane hasła, które zostało automatycznie zakazane dzięki możliwościom zakazane wykrywania hasła firmy Microsoft znalezieniem zbyt popularne lub szczególnie słabe.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>Typ działania: Self służyć postępu działań przepływu resetowania hasła

Poniżej wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje każdego kroku określonego użytkownika obejmującego (takich jak przekazywanie określonego hasła zresetować bramę uwierzytelniania) jako część hasło procesu resetowania.
* **Działanie aktora** -przepływu zresetować użytkownika, który wykonał część hasło. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** -przepływu zresetować użytkownika, który wykonał część hasło. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
  * _Powodzenie_ -wskazuje użytkownika zostało pomyślnie ukończone określonego kroku przepływu resetowania hasła.
  * _Błąd_ -wskazuje określonego kroku hasła resetować przepływu nie powiodło się. Kliknięcie przycisku wiersz umożliwia zobacz **przyczyny stanu działania** kategorię, aby dowiedzieć się więcej na temat przyczyny błędu.
* **Dozwolone przyczyny stanu działania**
  * Zobacz tabelę poniżej, aby [wszystkie dozwolone aktywności resetowania przyczyny stanu](#allowed-values-for-details-column)

### <a name="activity-type-unlock-user-account-self-service"></a>Typ działania: odblokować konto użytkownika (internetowy)

Poniżej wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje użytkownik pomyślnie odblokowane swojego konta usługi Active Directory bez zresetowania hasła z [Portal resetowania hasła programu Azure AD](https://passwordreset.microsoftonline.com) przy użyciu konta AD odblokowanie bez konieczności resetowania Funkcja.
* **Działanie aktora** — użytkownik, który odblokowane ich kont bez zresetowania hasła. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** — użytkownik, który odblokowane ich kont bez zresetowania hasła. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
  * _Powodzenie_ -wskazuje użytkownik pomyślnie odblokowane własne konto
  * _Błąd_ — wskazuje, nie można odblokować konto użytkownika. Kliknięcie przycisku wiersz umożliwia zobacz **przyczyny stanu działania** kategorię, aby dowiedzieć się więcej na temat przyczyny błędu.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Typ działania: użytkownik jest zarejestrowany dla samoobsługowego resetowania hasła

Poniżej wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje, użytkownik ma wszystkie wymagane informacje, aby można było do zresetowania swojego hasła zgodnie z obecnie określonego dzierżawcę zasady resetowania hasła. 
* **Działanie aktora** — użytkownik, który zarejestrował do resetowania hasła. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** — użytkownik, który zarejestrował do resetowania hasła. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
  * _Powodzenie_ -wskazuje pomyślnie zarejestrowany do resetowania zgodnie z zasadami bieżącego hasła użytkownika. 
  * _Błąd_ — wskazuje, nie można zarejestrować do resetowania hasła użytkownika. Kliknięcie przycisku wiersz umożliwia zobacz **przyczyny stanu działania** kategorię, aby dowiedzieć się więcej na temat przyczyny błędu. Uwaga - oznacza to, jeśli nie można zresetować swoje hasła, tylko, że nie zakończyła procesu rejestracji. Jeśli niezweryfikowane dane na koncie jest prawidłowa (takich jak numer telefonu, który nie jest sprawdzana poprawność), nawet jeśli ich nie została zweryfikowana ten numer telefonu, ich go użyć do zresetowania swojego hasła. Aby uzyskać więcej informacji, zobacz [co się dzieje, gdy użytkownik rejestruje?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="next-steps"></a>Następne kroki

Poniższe linki dają dostęp do dodatkowych informacji dotyczących resetowania haseł za pomocą usługi Azure AD

* [Skrót do dzienników inspekcji zarządzania użytkownika](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit) — przejdź bezpośrednio do zarządzania użytkownikami w Twojej dzierżawy dzienniki inspekcji
* [**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD 
* [**Licencjonowanie**](active-directory-passwords-licensing.md) — Konfigurowanie licencjonowania w usłudze Azure AD
* [**Dane**](active-directory-passwords-data.md) — Omówienie wymaganych danych i sposobu ich wykorzystania w zarządzaniu hasłami
* [**Wdrażanie**](active-directory-passwords-best-practices.md) — Planowanie funkcji samoobsługowego resetowania haseł i jej wdrażanie dla użytkowników przy użyciu znajdujących się tu wytycznych
* [**Dostosowywanie**](active-directory-passwords-customize.md) — Dostosowywanie wyglądu i działania środowiska samoobsługowego resetowania haseł dla firmy
* [**Szczegóły techniczne**](active-directory-passwords-how-it-works.md) — Informacje o tym, co dzieje się za kulisami tej funkcji i jak ona działa
* [**Często zadawane pytania**](active-directory-passwords-faq.md) — Jak? Dlaczego? Co? Gdzie? Kto? Kiedy? — Odpowiedzi na wszystkie nurtujące Cię pytania
* [**Rozwiązywanie problemów**](active-directory-passwords-troubleshoot.md) — Informacje o tym, jak rozwiązywać typowe problemy z samoobsługowym resetowaniem haseł
* [**Zasady**](active-directory-passwords-policy.md) — Omówienie zasad haseł usługi Azure AD i ich ustawianie
