---
title: "Get Insights: Raporty zarządzania hasłami w usłudze Azure AD | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse raporty tooget wgląd w operacji zarządzania hasło w Twojej organizacji."
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 1472b51d-53f4-4b0f-b1be-57f6fa88fa65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 90e0b8e621cdfe3e3a2f15df7b98115008855500
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-operational-insights-with-password-management-reports"></a>Jak raporty tooget usługi operational insights z zarządzania hasłami
> [!IMPORTANT]
> **Jesteś tutaj, ponieważ masz problemy z logowaniem?** Jeśli tak, [w tym miejscu opisano, jak zmienić i zresetować własne hasło](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
>
>

W tej sekcji opisano, jak używasz usługi Azure Active Directory Zarządzanie hasłami raporty tooview, jak użytkownicy korzystają z resetowania hasła i zmiany w Twojej organizacji.

* [**Omówienie raporty zarządzania hasła**](#overview-of-password-management-reports)
* [**Sposób zarządzania hasłami tooview raporty w programie hello nowego portalu Azure**](#how-to-view-password-management-reports)
 * [Ról katalogu dozwolone tooread raportów](#directory-roles-allowed-to-read-reports)
* [**Samoobsługowe zarządzanie hasłami działania typów w hello nowego portalu Azure**](#self-service-password-management-activity-types)
 * [Zablokowano dostęp do samodzielnego resetowania hasła](#activity-type-blocked-from-self-service-password-reset)
 * [Zmień hasło (internetowy)](#activity-type-change-password-self-service)
 * [Resetowanie hasła (Administrator)](#activity-type-reset-password-by-admin)
 * [Resetowanie hasła (internetowy)](#activity-type-reset-password-self-service)
 * [Resetowania hasła Self służą postępu działań przepływu](#activity-type-self-serve-password-reset-flow-activity-progress)
 * [Odblokować konto użytkownika (internetowy)](#activity-type-unlock-user-account-self-service)
 * [Użytkownik jest zarejestrowany dla samoobsługowego resetowania hasła](#activity-type-user-registered-for-self-service-password-reset)
* [**Jak tooretrieve hasło zarządzania zdarzenia z hello raportów usługi Azure AD i interfejsu API zdarzenia**](#how-to-retrieve-password-management-events-from-the-azure-ad-reports-and-events-api)
 * [Ograniczenia pobierania danych interfejsu API raportowania](#reporting-api-data-retrieval-limitations)
* [**Sposób hasła toodownload resetowania rejestracji zdarzeń szybko przy użyciu programu PowerShell**](#how-to-download-password-reset-registration-events-quickly-with-powershell)
* [**Sposób zarządzania hasłami tooview raportów w portalu klasycznym hello**](#how-to-view-password-management-reports-in-the-classic-portal)
* [**Działanie rejestracji w Twojej organizacji w klasycznym portalu hello resetowania hasła widoku**](#view-password-reset-registration-activity-in-the-classic-portal)
* [**Aktywność w Twojej organizacji w klasycznym portalu hello resetowania haseł widoku**](#view-password-reset-activity-in-the-classic-portal)


## <a name="overview-of-password-management-reports"></a>Omówienie raporty zarządzania hasła
Po wdrożeniu resetowania hasła jest jedną z najbardziej typowych następne kroki hello toosee jak jest używany w organizacji.  Na przykład może być tooget wgląd w sposób rejestracji użytkowników do resetowania hasła lub hasło, ile resetuje zostały wykonane w hello ostatnich kilku dni.  Poniżej przedstawiono niektóre hello często zadawane pytania, które będą mogli tooanswer z hello raporty zarządzania hasło, które istnieją w hello [portalu zarządzania Azure](https://manage.windowsazure.com) dzisiaj:

* Ile osób zarejestrowano do resetowania hasła?
* Kto został zarejestrowany do resetowania hasła?
* Jakie dane osób rejestracji?
* Ile osób do resetowania haseł w hello ostatnich 7 dni
* Co to są hello najbardziej typowe metody użytkownicy lub Administratorzy tooreset swoje hasła?
* Jakie są typowe problemy krój użytkowników lub administratorów, podczas próby toouse resetowania hasła?
* Jakie Administratorzy są często Resetowanie własnych haseł?
* Czy istnieje wszelkich podejrzanych działań z przejściem z funkcją resetowania hasła?

## <a name="how-tooview-password-management-reports"></a>W jaki sposób raporty zarządzania hasłami tooview
W nowych hello [Azure Portal](https://portal.azure.com) występują, mamy ulepszone sposób tooview resetowania i hasło rejestracji raport aktywności resetowania haseł.  Wykonaj kroki hello poniżej resetowania hasła hello toofind i hasło resetowania rejestracji zdarzeń w nowych hello [Azure Portal](https://portal.azure.com):

1. Przejdź za[**portal.azure.com**](https://portal.azure.com)
2. Polecenie hello **więcej usług** menu na powitania głównej nawigacji po lewej stronie portalu Azure
3. Wyszukaj **usługi Azure Active Directory** w hello listę usług i wybierz ją
4. Polecenie **użytkownicy i grupy** menu nawigacji hello Azure Active Directory
5. Polecenie hello **dzienników inspekcji** element nawigacji w menu nawigacji hello użytkownicy i grupy. Spowoduje to wyświetlenie wszystkich hello inspekcji zdarzeń występujących względem wszystkich użytkowników hello w katalogu. Można filtrować wszystkie hello hasła zdarzenia związane z, a także toosee tego widoku.
6. toofilter związane z zarządzaniem hasłami tego widoku tooonly hello zdarzenia, kliknij hello **filtru** u góry hello hello bloku.
7. Z hello **filtru** menu, wybierz hello **kategorii** listy rozwijanej i zmień je toohello **Samoobsługowe zarządzanie hasłami** typu kategorii.
8. Opcjonalnie dalsze listy hello filtrów przez wybranie określonych hello **działania** myślisz
### <a name="direct-link-toouser-audit-blade"></a>Bezpośrednie połączenie tooUser inspekcji bloku
Jeśli użytkownik jest zarejestrowany w portalu tooyour, w tym miejscu jest blok inspekcji użytkownika toohello bezpośredniego łącza umożliwia wyświetlenie te zdarzenia:

* [Przejdź bezpośrednio zarządzania toouser widok inspekcji](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit)

### <a name="directory-roles-allowed-tooread-reports"></a>Ról katalogu dozwolone tooread raportów
Obecnie hello następujących ról katalogu może odczytać raportów usługi Azure AD Password Management w klasycznym portalu Azure hello:

* Administrator globalny

Przed tooread stanie te raporty, administrator globalny w firmie hello musi mieć nie zgłoszono — w przypadku tego toobe dane pobierane w imieniu organizacji hello odwiedzając hello raportowania dzienniki tab lub inspekcji co najmniej raz. Do tej czynności dane nie będą zbierane dla Twojej organizacji.

więcej informacji o katalogu ról i co można zrobić Zobacz tooread [przypisywanie ról administratorów w usłudze Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-assign-admin-roles).

## <a name="self-service-password-management-activity-types"></a>Samoobsługowe zarządzanie hasłami typów działań
następujące typy działań Hello są wyświetlane w hello **Samoobsługowe zarządzanie hasłami** kategorii zdarzeń inspekcji.  Opis każdego z nich jest zgodna.

* [**Zablokowano dostęp do samodzielnego resetowania hasła** ](#activity-type-blocked-from-self-service-password-reset) -wskazuje użytkownik podjął próbę tooreset hasła, użyj określonej bramy lub sprawdzić poprawności numeru telefonu więcej niż 5 razy całkowita w ciągu 24 godzin.
* [**Zmień hasło (internetowy)** ](#activity-type-change-password-self-service) — wskazuje użytkownika wykonywane dobrowolny lub wymusić (z powodu tooexpiry) zmiany hasła.
* [**Zresetuj hasło (Administrator)** ](#activity-type-reset-password-by-admin) — określa administrator wykonane resetowania w imieniu użytkownika z portalu Azure hello hasła.
* [**Zresetuj hasło (internetowy)** ](#activity-type-reset-password-self-service) -wskazuje użytkownik pomyślnie zresetowano hasło z hello [Portal resetowania hasła programu Azure AD](https://passwordreset.microsoftonline.com).
* [**Resetowania hasła Self służą postępu działań przepływu** ](#activity-type-self-serve-password-reset-flow-activity-progress) -wskazuje każdego kroku określonego użytkownika obejmującego (takich jak przekazywanie określonego hasła zresetować bramę uwierzytelniania), jako część hasła hello procesu resetowania.
* [**Odblokować konto użytkownika (internetowy)** ](#activity-type-unlock-user-account-self-service) -wskazuje użytkownik pomyślnie odblokowane swoje konto usługi Active Directory bez potrzeby resetowania hasła z hello [Portal resetowania hasła programu Azure AD](https://passwordreset.microsoftonline.com) przy użyciu hello [odblokowanie konta AD bez konieczności resetowania](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) funkcji.
* [**Użytkownik jest zarejestrowany dla Samoobsługowe Resetowanie hasła** ](#activity-type-user-registered-for-self-service-password-reset) — wskazuje, użytkownik ma wszystkie wymagane hello informacji toobe stanie tooreset hasło zgodnie z zasady resetowania hasła obecnie określone dzierżawy hello.

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
 * _Powodzenie_ -wskazuje użytkownik pomyślnie zmieniono jego hasła
 * _Błąd_ — wskazuje, użytkownik nie toochange własnego hasła. Klikając wiersz hello pozwoli toosee hello **przyczyny stanu działania** więcej informacji na temat przyczyny wystąpił błąd hello toolearn kategorii.
* **Przyczyna niepowodzenia stanu działania** -
 * _FuzzyPolicyViolationInvalidPassword_ -hello użytkownik wybrał hasła, które zostało automatycznie zakazane powodu możliwości zakazane wykrywania hasła w tooMicrosoft znalezieniem toobe zbyt popularne lub szczególnie słabe.

### <a name="activity-type-reset-password-by-admin"></a>Typ działania: resetowania hasła (Administrator)
następujące listy Hello wyjaśniono tego działania szczegółowo:

* **Opis działania** — określa administrator wykonane resetowania w imieniu użytkownika z portalu Azure hello hasła.
* **Działanie aktora** -hello administratora, który wykonał hasła hello zresetować w imieniu innego użytkownika lub administratora. Musi być administratorem globalnym, hasło administratora, administrator użytkownika albo administratora pomocy technicznej.
* **Działania docelowego** -hello użytkownika, którego hasło zostało zresetowane. Może być użytkownika końcowego lub innego administratora.
* **Stany dozwolone działania**
 * _Powodzenie_ — wskazuje, jak administrator pomyślnie zresetowano hasło użytkownika
 * _Błąd_ — wskazuje, jak administrator nie toochange hasła użytkownika. Klikając wiersz hello pozwoli toosee hello **przyczyny stanu działania** więcej informacji na temat przyczyny wystąpił błąd hello toolearn kategorii.

### <a name="activity-type-reset-password-self-service"></a>Typ działania: resetowania hasła (internetowy)
następujące listy Hello wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje użytkownik pomyślnie zresetowano hasło z hello [Portal resetowania hasła programu Azure AD](https://passwordreset.microsoftonline.com).
* **Działanie aktora** — użytkownik hello zresetować swoje hasło. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** — użytkownik hello zresetować swoje hasło. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
 * _Powodzenie_ -wskazuje użytkownik pomyślnie zresetować własnego hasła.
 * _Błąd_ — wskazuje, użytkownik nie tooreset własnego hasła. Klikając wiersz hello pozwoli toosee hello **przyczyny stanu działania** więcej informacji na temat przyczyny wystąpił błąd hello toolearn kategorii.
* **Przyczyna niepowodzenia stanu działania** -
 * _FuzzyPolicyViolationInvalidPassword_ — Witaj, Administratorze wybrane hasło, które zostało automatycznie zakazane powodu możliwości zakazane wykrywania hasła w tooMicrosoft znalezieniem toobe zbyt popularne lub szczególnie słabe.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>Typ działania: Self służyć postępu działań przepływu resetowania hasła
następujące listy Hello wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje każdego kroku określonego użytkownika obejmującego (takich jak przekazywanie określonego hasła zresetować bramę uwierzytelniania) jako część hasła hello procesu resetowania.
* **Działanie aktora** -hello użytkownika, który wykonał część hasła hello zresetować przepływu. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** -hello użytkownika, który wykonał część hasła hello zresetować przepływu. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
 * _Powodzenie_ -wskazuje użytkownika zostało pomyślnie ukończone określonego kroku przepływu resetowania hasła hello.
 * _Błąd_ -wskazuje określonego kroku hasła hello resetować przepływu nie powiodło się. Klikając wiersz hello pozwoli toosee hello **przyczyny stanu działania** więcej informacji na temat przyczyny wystąpił błąd hello toolearn kategorii.
* **Dozwolone przyczyny stanu działania**
 * Zobacz tabelę poniżej, aby [wszystkie dozwolone aktywności resetowania przyczyny stanu](#allowed-values-for-details-column)

### <a name="activity-type-unlock-user-account-self-service"></a>Typ działania: odblokować konto użytkownika (internetowy)
następujące listy Hello wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje użytkownik pomyślnie odblokowane swoje konto usługi Active Directory bez potrzeby resetowania hasła z hello [Portal resetowania hasła programu Azure AD](https://passwordreset.microsoftonline.com) przy użyciu hello [AD odblokowywanie kont bez resetowania](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) funkcji.
* **Działanie aktora** — użytkownik hello odblokowane swojego konta bez zresetowania hasła. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** — użytkownik hello odblokowane swojego konta bez zresetowania hasła. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
 * _Powodzenie_ -wskazuje użytkownik pomyślnie odblokowane swojego konta
 * _Błąd_ — wskazuje, użytkownik nie toounlock swojego konta. Klikając wiersz hello pozwoli toosee hello **przyczyny stanu działania** więcej informacji na temat przyczyny wystąpił błąd hello toolearn kategorii.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Typ działania: użytkownik jest zarejestrowany dla samoobsługowego resetowania hasła
następujące listy Hello wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje, użytkownik ma wszystkie wymagane hello informacji toobe stanie tooreset hasło zgodnie z zasady resetowania hasła obecnie określone dzierżawy hello.
* **Działanie aktora** -hello użytkownik zarejestrowany w celu resetowania haseł. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** -hello użytkownik zarejestrowany w celu resetowania haseł. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
 * _Powodzenie_ -wskazuje użytkownik pomyślnie zarejestrowany do resetowania zgodnie z zasadami bieżącego hello hasła.
 * _Błąd_ -wskazuje tooregister użytkownika nie powiodło się, w celu resetowania haseł. Klikając wiersz hello pozwoli toosee hello **przyczyny stanu działania** więcej informacji na temat przyczyny wystąpił błąd hello toolearn kategorii. Uwaga - oznacza to użytkownik jest nie jest w stanie tooreset własnego hasła, wystarczy, że użytkownik nie została ukończona hello procesu rejestracji. Jeśli niezweryfikowane dane na koncie jest prawidłowa (takich jak numer telefonu, który nie jest sprawdzana poprawność), nawet jeśli ich nie została zweryfikowana ten numer telefonu, mogą nadal go używać tooreset swoje hasło. Aby uzyskać więcej informacji, zobacz [co się dzieje, gdy użytkownik rejestruje?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="how-tooretrieve-password-management-events-from-hello-azure-ad-reports-and-events-api"></a>Jak tooretrieve hasło zarządzania zdarzenia z hello raportów usługi Azure AD i interfejsu API zdarzenia
Począwszy od sierpnia 2015 raporty hello Azure AD i interfejsu API zdarzenia obsługuje teraz wszystkie hello informacje zawarte w hello hasła resetowania hasła resetowania rejestracji raportów i pobierania. Przy użyciu tego interfejsu API, można pobrać resetowania hasła poszczególnych i resetowania hasła rejestrowania zdarzeń dla integracji z hello technologii choce Twojego raportowania.

### <a name="how-tooget-started-with-hello-reporting-api"></a>Jak tooget pracę z interfejsem API raportowania hello
tooaccess te dane będą potrzebne toowrite małych aplikacji lub skryptu tooretrieve z naszych serwerów. [Dowiedz się, jak tooget wprowadzenie hello Azure AD interfejsu API raportowania](active-directory-reporting-api-getting-started.md).

Po utworzeniu skryptu pracy, następnie należy tooexamine hello hasła resetowania rejestracji zdarzeń i że można pobrać toomeet scenariuszy.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): Wyświetla kolumny hello dostępne dla zdarzeń resetowania hasła
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): Wyświetla listę dostępnych kolumn hello dla zdarzenia rejestracji resetowania hasła

### <a name="reporting-api-data-retrieval-limitations"></a>Ograniczenia pobierania danych interfejsu API raportowania
Obecnie hello raportów usługi Azure AD i interfejsu API zdarzenia pobiera się zbyt**75,000 pojedynczych zdarzeń** z hello [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) i [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) typów , obejmujących hello **ostatnich 30 dni**.

Jeśli konieczne tooretrieve lub przechowywania danych po przekroczeniu tego okna, zalecamy utrwalanie go w zewnętrznej bazy danych i przy użyciu hello interfejsu API tooquery hello delty, które powodują. Najlepszym rozwiązaniem jest toobegin pobierania tych danych podczas uruchamiania hasło zresetować procesu rejestracji w firmie, utrwalić go zewnętrznie, a następnie przejdź do przodu tootrack hello delty z tego punktu.

## <a name="how-toodownload-password-reset-registration-events-quickly-with-powershell"></a>Sposób hasła toodownload resetowania rejestracji zdarzeń szybko przy użyciu programu PowerShell
Ponadto toousing hello raportów usługi Azure AD i interfejsu API zdarzenia bezpośrednio, można także użyć hello poniżej zdarzenia rejestracji toorecent skrypt programu PowerShell w katalogu. Jest przydatne w przypadku, gdy chcesz toosee, który został ostatnio zarejestrowany lub chcesz tooensure, że wdrożenie resetowania hasła jest wykonywana zgodnie z oczekiwaniami.

* [Skrypt programu PowerShell działania rejestracji usługi Azure AD SSPR](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

## <a name="how-tooview-password-management-reports-in-hello-classic-portal"></a>Sposób zarządzania hasłami tooview raportów w portalu klasycznym hello
Raporty zarządzania toofind hello hasła, wykonaj kroki hello poniżej:

1. Polecenie hello **usługi Active Directory** rozszerzenia hello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Z listy hello, która jest wyświetlana w portalu hello, wybierz swój katalog.
3. Polecenie hello **raporty** kartę.
4. Sprawdź w obszarze hello **Dzienniki aktywności** sekcji.
5. Wybierz albo hello **aktywność resetowania haseł** raportu lub hello **aktywność rejestracji resetowania haseł** raportu.

## <a name="view-password-reset-registration-activity-in-hello-classic-portal"></a>Działanie rejestracji w portalu klasycznym hello resetowania hasła widoku
raport aktywności rejestracji resetowania haseł Hello pokazuje resetowania hasła wszystkich rejestracji, które wystąpiły w Twojej organizacji.  Rejestracji resetowania hasła jest wyświetlany w tym raporcie dla portalu rejestracji resetowania każdy użytkownik, który został pomyślnie zarejestrowany informacje dotyczące uwierzytelniania na powitania hasła ([http://aka.ms/ssprsetup](http://aka.ms/ssprsetup)).

* **Maksymalny przedział czasu**: 30 dni
* **Maksymalna liczba wierszy**: 75 000
* **Do pobrania**: tak, przy użyciu pliku CSV

### <a name="description-of-report-columns"></a>Opis kolumn raportu
Witaj poniżej objaśniono kolumn raportu hello szczegółowo:

* **Użytkownik** — użytkownik hello, które próbowały hasła zresetować operacji rejestracji.
* **Rola** — Witaj rolę użytkownika hello w katalogu hello.
* **Data i godzina** — hello Data i godzina próby hello.
* **Dane zarejestrowane** — rejestracja resetowania podane podczas hasło użytkownika hello danych uwierzytelniania.

### <a name="description-of-report-values"></a>Opis raportu wartości
Witaj poniższej tabeli opisano różne wartości hello dozwolone dla każdej kolumny:

| Kolumna | Dozwolone wartości i ich znaczenie |
| --- | --- |
| Data zarejestrowana |**Alternatywny adres E-mail** — użytkownik alternatywny adres e-mail lub uwierzytelniania wiadomości e-mail tooauthenticate<p><p>**Telefon biurowy**— office phone tooauthenticate używać użytkownika<p>**Telefon komórkowy** -tooauthenticate phone telefon komórkowy lub uwierzytelniania używać użytkownika<p>**Pytania zabezpieczające** — tooauthenticate pytania zabezpieczeń użytkownika używane<p>**Dowolną kombinację hello powyżej (np. alternatywny adres E-mail + telefon komórkowy)** — występuje, gdy zasady 2 bramy jest określona i pokazuje, które dwie metody hello tooauthentication użytkownika używany żądanie zresetowania hasła. |

## <a name="view-password-reset-activity-in-hello-classic-portal"></a>Aktywność w portalu klasycznym hello resetowania haseł widoku
Ten raport przedstawia resetowania hasła wszystkich prób, które wystąpiły w Twojej organizacji.

* **Maksymalny przedział czasu**: 30 dni
* **Maksymalna liczba wierszy**: 75 000
* **Do pobrania**: tak, przy użyciu pliku CSV

### <a name="description-of-report-columns"></a>Opis kolumn raportu
Witaj poniżej objaśniono kolumn raportu hello szczegółowo:

1. **Użytkownik** — użytkownik hello, które próbowały hasła zresetować operacji (na podstawie hello identyfikator użytkownika pola pod warunkiem, gdy użytkownik hello tooreset hasła).
2. **Rola** — Witaj rolę użytkownika hello w katalogu hello.
3. **Data i godzina** — hello Data i godzina próby hello.
4. **Używane metody** — użytkownik hello metod uwierzytelniania to resetowania operacji.
5. **Wynik** — operacji resetowania wynik końcowy hello hello hasła.
6. **Szczegóły** — szczegóły hello Dlaczego resetowania hasła hello spowodowała wartość hello jak.  Zawiera również wszystkie kroki zaradcze może potrwać tooresolve wystąpił nieoczekiwany błąd.

### <a name="description-of-report-values"></a>Opis raportu wartości
Witaj poniższej tabeli opisano różne wartości hello dozwolone dla każdej kolumny:

| Kolumna | Dozwolone wartości i ich znaczenie |
| --- | --- |
| Metody stosowane |**Alternatywny adres E-mail** — użytkownik alternatywny adres e-mail lub uwierzytelniania wiadomości e-mail tooauthenticate<p>**Telefon biurowy** — office phone tooauthenticate używać użytkownika<p>**Telefon komórkowy** — tooauthenticate phone telefon komórkowy lub uwierzytelniania używać użytkownika<p>**Pytania zabezpieczające** — tooauthenticate pytania zabezpieczeń użytkownika używane<p>**Dowolną kombinację hello powyżej (np. alternatywny adres E-mail + telefon komórkowy)** — występuje, gdy zasady 2 bramy jest określona i pokazuje, które dwie metody hello tooauthentication użytkownika używany żądanie zresetowania hasła. |
| wynik |**Porzucone** — użytkownika uruchomiony resetowania hasła, ale został zatrzymany połowie, za pośrednictwem, przerywając<p>**Zablokowane** — konto użytkownika zostało resetowania powodu stronę resetowania hasła hello toouse tooattempting hasła uniemożliwił toouse lub jednego hasła zresetować bramy zbyt wiele razy w okresie 24 godzin.<p>**Anulowane** — uruchomiona resetowania hasła użytkownika, ale następnie kliknięto pozycję sesji hello toocancel hello przycisk Anuluj, które zostały części sposób za pomocą <p>**Skontaktować się z administratorem** — użytkownika wystąpił problem podczas jego sesji, które on nie można rozpoznać, więc hello użytkownik kliknął link "Skontaktuj się z administratorem" hello, zamiast Kończenie hasła hello resetowania przepływu<p>**Nie powiodło się** — użytkownik nie stanie tooreset hasła, prawdopodobnie ponieważ użytkownik hello nie został skonfigurowany toouse hello funkcji (np. Brak licencji, Brak informacji uwierzytelniania hasła zarządzane lokalnego, ale zapisywania zwrotnego jest wyłączone).<p>**Pomyślnie** — resetowania hasła zakończyło się pomyślnie. |
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

## <a name="next-steps"></a>Następne kroki
Poniżej przedstawiono tooall łącza z hello stron z dokumentacją resetowania hasła programu Azure AD:

* **Jesteś tutaj, ponieważ masz problemy z logowaniem?** Jeśli tak, [w tym miejscu opisano, jak zmienić i zresetować własne hasło](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
* [**Jak działa** ](active-directory-passwords-how-it-works.md) — Dowiedz się więcej o hello sześciu różnych komponentach usługi hello i co działają
* [**Wprowadzenie** ](active-directory-passwords-getting-started.md) — Dowiedz się, jak tooallow tooreset użytkowników i zmieniać hasła chmurze lub lokalnie
* [**Dostosowywanie** ](active-directory-passwords-customize.md) — Dowiedz się wygląd toocustomize hello & sposób działania i zachowanie hello usługi musi mieć tooyour organizacji
* [**Najlepsze rozwiązania** ](active-directory-passwords-best-practices.md) — Dowiedz się, jak wdrożyć i efektywnie zarządzać hasłami w organizacji w tooquickly
* [**Często zadawane pytania dotyczące** ](active-directory-passwords-faq.md) -odpowiedzi toofrequently zadawane pytania
* [**Rozwiązywanie problemów z** ](active-directory-passwords-troubleshoot.md) — Dowiedz się, jak tooquickly Rozwiązywanie problemów z usługą hello
* [**Dowiedz się więcej** ](active-directory-passwords-learn-more.md) — zgłębiaj szczegóły techniczne hello działania usługi hello
