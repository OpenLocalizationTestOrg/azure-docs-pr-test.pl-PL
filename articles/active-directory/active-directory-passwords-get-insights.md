---
title: "Get Insights: Raporty zarządzania hasłami w usłudze Azure AD | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak używać raportów do uzyskiwanie wglądu w operacji zarządzania hasło w Twojej organizacji."
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
ms.openlocfilehash: ae83df618e3c392fe89878bcd1be0d6c6cb1edb4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-get-operational-insights-with-password-management-reports"></a>Aby uzyskać szczegółowe dane operacyjne z zarządzaniem hasłami raportów
> [!IMPORTANT]
> **Jesteś tutaj, ponieważ masz problemy z logowaniem?** Jeśli tak, [w tym miejscu opisano, jak zmienić i zresetować własne hasło](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
>
>

W tej sekcji opisano, jak można użyć raportów zarządzania hasła usługi Azure Active Directory do wyświetlania, jak użytkownicy korzystają z resetowania hasła i zmiany w Twojej organizacji.

* [**Omówienie raporty zarządzania hasła**](#overview-of-password-management-reports)
* [**Jak wyświetlić raporty zarządzania hasło w portalu Azure**](#how-to-view-password-management-reports)
 * [Role katalogu mogą odczytywać raportów](#directory-roles-allowed-to-read-reports)
* [**Samoobsługowe zarządzanie hasłami działania typów w nowego portalu Azure**](#self-service-password-management-activity-types)
 * [Zablokowano dostęp do samodzielnego resetowania hasła](#activity-type-blocked-from-self-service-password-reset)
 * [Zmień hasło (internetowy)](#activity-type-change-password-self-service)
 * [Resetowanie hasła (Administrator)](#activity-type-reset-password-by-admin)
 * [Resetowanie hasła (internetowy)](#activity-type-reset-password-self-service)
 * [Resetowania hasła Self służą postępu działań przepływu](#activity-type-self-serve-password-reset-flow-activity-progress)
 * [Odblokować konto użytkownika (internetowy)](#activity-type-unlock-user-account-self-service)
 * [Użytkownik jest zarejestrowany dla samoobsługowego resetowania hasła](#activity-type-user-registered-for-self-service-password-reset)
* [**Jak pobrać hasło zdarzeń zarządzania raportów usługi Azure AD i interfejsu API zdarzenia**](#how-to-retrieve-password-management-events-from-the-azure-ad-reports-and-events-api)
 * [Ograniczenia pobierania danych interfejsu API raportowania](#reporting-api-data-retrieval-limitations)
* [**Jak pobrać zdarzenia rejestracji resetowania haseł szybko przy użyciu programu PowerShell**](#how-to-download-password-reset-registration-events-quickly-with-powershell)
* [**Jak wyświetlić raporty zarządzania hasło w klasycznym portalu**](#how-to-view-password-management-reports-in-the-classic-portal)
* [**Aktywność rejestracji w Twojej organizacji w klasycznym portalu resetowania haseł widoku**](#view-password-reset-registration-activity-in-the-classic-portal)
* [**Aktywność w Twojej organizacji w klasycznym portalu resetowania haseł widoku**](#view-password-reset-activity-in-the-classic-portal)


## <a name="overview-of-password-management-reports"></a>Omówienie raporty zarządzania hasła
Po wdrożeniu resetowania hasła jest jedną z najbardziej typowych następne kroki aby zobaczyć, jak jest używany w organizacji.  Na przykład możesz uzyskać wgląd w sposób rejestracji użytkowników do resetowania hasła lub hasło, ile resetuje zostały wykonane w ciągu ostatnich kilku dni.  Poniżej przedstawiono niektóre często zadawane pytania, które będą mogli odpowiedzieć raporty zarządzania hasło, które istnieją w [portalu zarządzania Azure](https://manage.windowsazure.com) dzisiaj:

* Ile osób zarejestrowano do resetowania hasła?
* Kto został zarejestrowany do resetowania hasła?
* Jakie dane osób rejestracji?
* Ile osób do resetowania hasła w ciągu ostatnich 7 dni
* Co to są najbardziej typowe metody użytkowników lub administratorów za pomocą resetowanie haseł?
* Jakie są typowe problemy użytkownicy lub Administratorzy krój podczas próby użycia resetowania hasła?
* Jakie Administratorzy są często Resetowanie własnych haseł?
* Czy istnieje wszelkich podejrzanych działań z przejściem z funkcją resetowania hasła?

## <a name="how-to-view-password-management-reports"></a>Jak wyświetlić raporty zarządzania hasła
W nowym [Azure Portal](https://portal.azure.com) doświadczenia, będziemy mieć lepszą sposobem wyświetlenia resetowania hasła i rejestracji aktywność resetowania haseł.  Wykonaj poniższe kroki, aby znaleźć resetowania hasła i zdarzenia rejestracji resetowania haseł w nowym [Azure Portal](https://portal.azure.com):

1. Przejdź do [ **portal.azure.com**](https://portal.azure.com)
2. Polecenie **więcej usług** menu głównego nawigacji po lewej stronie portalu Azure
3. Wyszukaj **usługi Azure Active Directory** na liście usług i wybierz ją
4. Polecenie **użytkownicy i grupy** w menu nawigacyjnym usługi Azure Active Directory
5. Polecenie **dzienników inspekcji** element nawigacji w menu nawigacyjnym użytkownicy i grupy. Spowoduje to wyświetlenie wszystkich przetwarzanie zdarzeń inspekcji dla wszystkich użytkowników w katalogu. Ten widok, aby wyświetlić wszystkie powiązane hasło zdarzenia, a także można filtrować.
6. Aby filtrować tego widoku i tylko zdarzenia związane z zarządzaniem hasłami, kliknij przycisk **filtru** u góry bloku.
7. Z **filtru** menu, wybierz opcję **kategorii** listy rozwijanej i zmień go na **Samoobsługowe zarządzanie hasłami** typu kategorii.
8. Opcjonalnie dalsze Filtruj listę, wybierając konkretnym **działania** myślisz
### <a name="direct-link-to-user-audit-blade"></a>Bezpośredniego łącza do bloku inspekcji użytkownika
Jeśli logujesz się do portalu, w tym miejscu jest bezpośredniego łącza do bloku inspekcji użytkownika umożliwia wyświetlenie te zdarzenia:

* [Przejdź do widoku inspekcji zarządzania użytkownika bezpośrednio](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit)

### <a name="directory-roles-allowed-to-read-reports"></a>Role katalogu mogą odczytywać raportów
Obecnie następujące role katalogu może odczytać raportów usługi Azure AD Password Management w klasycznym portalu Azure:

* Administrator globalny

Aby można było odczytać te raporty, administratora globalnego firmy musi mieć zgłoszono — w przypadku te dane mają zostać pobrane w imieniu organizacji odwiedzając dzienników inspekcji lub tab raportowania co najmniej raz. Do tej czynności dane nie będą zbierane dla Twojej organizacji.

Aby dowiedzieć się więcej o rolach katalogu i co można zrobić, zobacz [przypisywanie ról administratorów w usłudze Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-assign-admin-roles).

## <a name="self-service-password-management-activity-types"></a>Samoobsługowe zarządzanie hasłami typów działań
Następujące typy działań są wyświetlane w **Samoobsługowe zarządzanie hasłami** kategorii zdarzeń inspekcji.  Opis każdego z nich jest zgodna.

* [**Zablokowano dostęp do samodzielnego resetowania hasła** ](#activity-type-blocked-from-self-service-password-reset) -wskazuje użytkownik próbował zresetować hasło, użyj określonych bramy lub sprawdzania poprawności numeru telefonu więcej niż 5 razy całkowita w ciągu 24 godzin.
* [**Zmień hasło (internetowy)** ](#activity-type-change-password-self-service) -wskazuje użytkownika wykonywane dobrowolny lub wymusić (z powodu wygaśnięcia) zmiany hasła.
* [**Zresetuj hasło (Administrator)** ](#activity-type-reset-password-by-admin) — określa administrator wykonane resetowania w imieniu użytkownika z portalu Azure hasła.
* [**Zresetuj hasło (internetowy)** ](#activity-type-reset-password-self-service) -wskazuje użytkownik pomyślnie zresetowano hasło z [Portal resetowania hasła programu Azure AD](https://passwordreset.microsoftonline.com).
* [**Resetowania hasła Self służą postępu działań przepływu** ](#activity-type-self-serve-password-reset-flow-activity-progress) -wskazuje każdego kroku określonego użytkownika obejmującego (takich jak przekazywanie określonego hasła zresetować bramę uwierzytelniania), jako część hasło procesu resetowania.
* [**Odblokować konto użytkownika (internetowy)** ](#activity-type-unlock-user-account-self-service) -wskazuje użytkownik pomyślnie odblokowane swoje konto usługi Active Directory bez potrzeby resetowania hasła z [Portal resetowania hasła programu Azure AD](https://passwordreset.microsoftonline.com) przy użyciu [odblokowanie konta AD bez konieczności resetowania](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) funkcji.
* [**Użytkownik jest zarejestrowany dla Samoobsługowe Resetowanie hasła** ](#activity-type-user-registered-for-self-service-password-reset) -wskazuje użytkownik zarejestrował wszystkie wymagane informacje, aby można było zresetować jego lub zasady resetowania swojego hasła zgodnie z obecnie określone dzierżawy hasła.

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
 * _Powodzenie_ -wskazuje użytkownik pomyślnie zmieniono jego hasła
 * _Błąd_ -wskazuje użytkownika nie można zmienić swoje hasło. Klikając wiersz umożliwi zobacz **przyczyny stanu działania** kategorię, aby dowiedzieć się więcej na temat przyczyny błędu.
* **Przyczyna niepowodzenia stanu działania** -
 * _FuzzyPolicyViolationInvalidPassword_ — użytkownik wybrał hasła, które zostało automatycznie zakazane dzięki możliwościom zakazane wykrywania hasła firmy Microsoft znalezieniem zbyt popularne lub szczególnie słabe.

### <a name="activity-type-reset-password-by-admin"></a>Typ działania: resetowania hasła (Administrator)
Poniżej wyjaśniono tego działania szczegółowo:

* **Opis działania** — określa administrator wykonane resetowania w imieniu użytkownika z portalu Azure hasła.
* **Działanie aktora** -administratora, który wykonał resetowania w imieniu innego użytkownika lub administratora hasła. Musi być administratorem globalnym, hasło administratora, administrator użytkownika albo administratora pomocy technicznej.
* **Działania docelowego** -użytkownika, którego hasło zostało zresetowane. Może być użytkownika końcowego lub innego administratora.
* **Stany dozwolone działania**
 * _Powodzenie_ — wskazuje, jak administrator pomyślnie zresetowano hasło użytkownika
 * _Błąd_ — wskazuje, jak administrator nie można zmienić hasła użytkownika. Klikając wiersz umożliwi zobacz **przyczyny stanu działania** kategorię, aby dowiedzieć się więcej na temat przyczyny błędu.

### <a name="activity-type-reset-password-self-service"></a>Typ działania: resetowania hasła (internetowy)
Poniżej wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje użytkownik pomyślnie zresetowano hasło z [Portal resetowania hasła programu Azure AD](https://passwordreset.microsoftonline.com).
* **Działanie aktora** — użytkownik, który zresetować swoje hasło. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** — użytkownik, który zresetować swoje hasło. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
 * _Powodzenie_ -wskazuje użytkownik pomyślnie zresetować własnego hasła.
 * _Błąd_ -wskazuje użytkownika nie można zresetować własnego hasła. Klikając wiersz umożliwi zobacz **przyczyny stanu działania** kategorię, aby dowiedzieć się więcej na temat przyczyny błędu.
* **Przyczyna niepowodzenia stanu działania** -
 * _FuzzyPolicyViolationInvalidPassword_ — administrator wybrane hasło, które zostało automatycznie zakazane dzięki możliwościom zakazane wykrywania hasła firmy Microsoft znalezieniem zbyt popularne lub szczególnie słabe.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>Typ działania: Self służyć postępu działań przepływu resetowania hasła
Poniżej wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje każdego kroku określonego użytkownika obejmującego (takich jak przekazywanie określonego hasła zresetować bramę uwierzytelniania) jako część hasło procesu resetowania.
* **Działanie aktora** -przepływu zresetować użytkownika, który wykonał część hasło. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** -przepływu zresetować użytkownika, który wykonał część hasło. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
 * _Powodzenie_ -wskazuje użytkownika zostało pomyślnie ukończone określonego kroku przepływu resetowania hasła.
 * _Błąd_ -wskazuje określonego kroku hasła resetować przepływu nie powiodło się. Klikając wiersz umożliwi zobacz **przyczyny stanu działania** kategorię, aby dowiedzieć się więcej na temat przyczyny błędu.
* **Dozwolone przyczyny stanu działania**
 * Zobacz tabelę poniżej, aby [wszystkie dozwolone aktywności resetowania przyczyny stanu](#allowed-values-for-details-column)

### <a name="activity-type-unlock-user-account-self-service"></a>Typ działania: odblokować konto użytkownika (internetowy)
Poniżej wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje użytkownik pomyślnie odblokowane swoje konto usługi Active Directory bez potrzeby resetowania hasła z [Portal resetowania hasła programu Azure AD](https://passwordreset.microsoftonline.com) przy użyciu [konta AD odblokowanie bez konieczności resetowania](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) funkcji.
* **Działanie aktora** — użytkownik, który odblokowane swojego konta bez zresetowania hasła. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** — użytkownik, który odblokowane swojego konta bez zresetowania hasła. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
 * _Powodzenie_ -wskazuje użytkownik pomyślnie odblokowane swojego konta
 * _Błąd_ — wskazuje, nie można odblokować swojego konta użytkownika. Klikając wiersz umożliwi zobacz **przyczyny stanu działania** kategorię, aby dowiedzieć się więcej na temat przyczyny błędu.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Typ działania: użytkownik jest zarejestrowany dla samoobsługowego resetowania hasła
Poniżej wyjaśniono tego działania szczegółowo:

* **Opis działania** — wskazuje użytkownik zarejestrował wszystkie wymagane informacje, aby można było zresetować jego lub zasady resetowania swojego hasła zgodnie z obecnie określone dzierżawy hasła.
* **Działanie aktora** — użytkownik, który zarejestrował do resetowania hasła. Może być użytkownik końcowy lub administrator.
* **Działania docelowego** — użytkownik, który zarejestrował do resetowania hasła. Może być użytkownik końcowy lub administrator.
* **Stany dozwolone działania**
 * _Powodzenie_ -wskazuje użytkownik, który został pomyślnie zarejestrowany do resetowania zgodnie z zasadami bieżącego hasła.
 * _Błąd_ — wskazuje, nie można zarejestrować do resetowania hasła użytkownika. Klikając wiersz umożliwi zobacz **przyczyny stanu działania** kategorię, aby dowiedzieć się więcej na temat przyczyny błędu. Uwaga - oznacza to, że użytkownik nie będzie można przywrócić jego lub swojego hasła, tak że dany użytkownik zakończył się proces rejestracji. Jeśli niezweryfikowane dane na koncie jest prawidłowa (takich jak numer telefonu, który nie jest sprawdzana poprawność), nawet jeśli ich nie została zweryfikowana ten numer telefonu, ich go użyć do zresetowania swojego hasła. Aby uzyskać więcej informacji, zobacz [co się dzieje, gdy użytkownik rejestruje?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="how-to-retrieve-password-management-events-from-the-azure-ad-reports-and-events-api"></a>Jak pobrać hasło zdarzeń zarządzania raportów usługi Azure AD i interfejsu API zdarzenia
Począwszy od sierpnia 2015 r. raportów usługi Azure AD i interfejsu API zdarzenia obsługuje teraz wszystkie informacje zawarte w hasło resetowania hasła resetowania rejestracji raportów i pobierania. Przy użyciu tego interfejsu API, można pobrać resetowania hasła poszczególnych i rejestracji zdarzeń dla integracji z technologią raportowania choce Twojego resetowania hasła.

### <a name="how-to-get-started-with-the-reporting-api"></a>Jak rozpocząć pracę z interfejsem API raportowania
Aby uzyskać dostęp do tych danych, należy napisać małych aplikacji lub skrypt, aby pobrać go ze swoich serwerów. [Dowiedz się, jak rozpocząć pracę z usługi Azure AD API raportowania](active-directory-reporting-api-getting-started.md).

Po utworzeniu skryptu pracy, następnie należy zbadać hasła resetowania i rejestracji zdarzenia, które można pobrać, aby spełnić scenariuszy.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): Wyświetla listę dostępnych kolumn zdarzeń resetowania hasła
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): Wyświetla listę dostępnych kolumn dla zdarzenia rejestracji resetowania hasła

### <a name="reporting-api-data-retrieval-limitations"></a>Ograniczenia pobierania danych interfejsu API raportowania
Obecnie raportów usługi Azure AD i interfejsu API zdarzenia pobiera do **75,000 pojedynczych zdarzeń** z [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) i [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) typów Łączenie węzłów **ostatnich 30 dni**.

Jeśli potrzebujesz do pobierania lub przechowywania danych po przekroczeniu tego okna, zalecamy utrwalanie go w zewnętrznej bazy danych i do badania delty, które powodują przy użyciu interfejsu API. Najlepszym rozwiązaniem jest rozpocząć pobieranie te dane po uruchomieniu hasło zresetować procesu rejestracji w firmie, utrwalić go zewnętrznie, a następnie kontynuuj do śledzenia może od tego momentu.

## <a name="how-to-download-password-reset-registration-events-quickly-with-powershell"></a>Jak pobrać zdarzenia rejestracji resetowania haseł szybko przy użyciu programu PowerShell
Oprócz bezpośrednio za pomocą raportów usługi Azure AD i interfejsu API zdarzenia, można także użyć poniższego skryptu programu PowerShell, aby ostatnie zdarzenia rejestracji w katalogu. Jest to przydatne w przypadku, gdy użytkownik chce zobaczyć, kto został ostatnio zarejestrowany lub chcesz upewnij się, że wdrożenia resetowania hasła jest wykonywana zgodnie z oczekiwaniami.

* [Skrypt programu PowerShell działania rejestracji usługi Azure AD SSPR](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

## <a name="how-to-view-password-management-reports-in-the-classic-portal"></a>Jak wyświetlić raporty zarządzania hasło w klasycznym portalu
Aby znaleźć raporty zarządzania hasła, wykonaj następujące czynności:

1. Polecenie **usługi Active Directory** rozszerzenia [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Z listy, która jest wyświetlana w portalu, wybierz swój katalog.
3. Polecenie **raporty** kartę.
4. Sprawdź w obszarze **Dzienniki aktywności** sekcji.
5. Wybierz opcję **aktywność resetowania haseł** raportu lub **aktywność rejestracji resetowania haseł** raportu.

## <a name="view-password-reset-registration-activity-in-the-classic-portal"></a>Aktywność rejestracji w klasycznym portalu resetowania haseł widoku
Raport aktywności rejestracji resetowania haseł przedstawia resetowania hasła wszystkich rejestracji, które wystąpiły w Twojej organizacji.  Rejestracji resetowania hasła jest wyświetlany w tym raporcie dla portalu rejestracji resetowania każdy użytkownik, który został pomyślnie zarejestrowany informacje o uwierzytelnianiu w hasło ([http://aka.ms/ssprsetup](http://aka.ms/ssprsetup)).

* **Maksymalny przedział czasu**: 30 dni
* **Maksymalna liczba wierszy**: 75 000
* **Do pobrania**: tak, przy użyciu pliku CSV

### <a name="description-of-report-columns"></a>Opis kolumn raportu
Poniżej objaśniono szczegółowo kolumn raportu:

* **Użytkownik** — operacja rejestracji zresetować użytkownika, które próbowały hasła.
* **Rola** — rola użytkownika w katalogu.
* **Data i godzina** — Data i godzina próby.
* **Dane zarejestrowane** — jakie dane uwierzytelniania użytkownika podana podczas hasło rejestracji resetowania.

### <a name="description-of-report-values"></a>Opis raportu wartości
W poniższej tabeli opisano różne wartości dla każdej kolumny:

| Kolumna | Dozwolone wartości i ich znaczenie |
| --- | --- |
| Data zarejestrowana |**Alternatywny adres E-mail** — użytkownika używany alternatywny adres e-mail lub uwierzytelniania wiadomości e-mail do uwierzytelniania<p><p>**Telefon biurowy**— telefon biurowy użytkownika służące do uwierzytelniania<p>**Telefon komórkowy** — użytkownik telefon komórkowy lub numer telefonu uwierzytelniania do uwierzytelniania<p>**Pytania zabezpieczające** — używane przez użytkownika pytań zabezpieczających do uwierzytelniania<p>**Dowolne z powyższych (np. alternatywny adres E-mail + telefon komórkowy)** — występuje, gdy zasady 2 bramy jest określona i przedstawia które dwie metody użytkownika służące do uwierzytelniania żądanie zresetowania hasła. |

## <a name="view-password-reset-activity-in-the-classic-portal"></a>Aktywność w klasycznym portalu resetowania haseł widoku
Ten raport przedstawia resetowania hasła wszystkich prób, które wystąpiły w Twojej organizacji.

* **Maksymalny przedział czasu**: 30 dni
* **Maksymalna liczba wierszy**: 75 000
* **Do pobrania**: tak, przy użyciu pliku CSV

### <a name="description-of-report-columns"></a>Opis kolumn raportu
Poniżej objaśniono szczegółowo kolumn raportu:

1. **Użytkownik** — użytkownik, które próbowały hasła zresetować operacji (na podstawie Identyfikatora użytkownika pola pod warunkiem, gdy użytkownik jest dostarczany do resetowania hasła).
2. **Rola** — rola użytkownika w katalogu.
3. **Data i godzina** — Data i godzina próby.
4. **Używane metody** — metod uwierzytelniania użytkownika używane przez ten zresetować operacji.
5. **Wynik** — w rezultacie hasła zresetować operacji.
6. **Szczegóły** — szczegóły Dlaczego zresetować hasła spowodowała jak wartość.  Obejmuje też kroki wszelkie środki zaradcze, może potrwać do rozpoznania wystąpił nieoczekiwany błąd.

### <a name="description-of-report-values"></a>Opis raportu wartości
W poniższej tabeli opisano różne wartości dla każdej kolumny:

| Kolumna | Dozwolone wartości i ich znaczenie |
| --- | --- |
| Metody stosowane |**Alternatywny adres E-mail** — użytkownika używany alternatywny adres e-mail lub uwierzytelniania wiadomości e-mail do uwierzytelniania<p>**Telefon biurowy** — telefon biurowy użytkownika służące do uwierzytelniania<p>**Telefon komórkowy** — użytkownik telefon komórkowy lub numer telefonu uwierzytelniania do uwierzytelniania<p>**Pytania zabezpieczające** — używane przez użytkownika pytań zabezpieczających do uwierzytelniania<p>**Dowolne z powyższych (np. alternatywny adres E-mail + telefon komórkowy)** — występuje, gdy zasady 2 bramy jest określona i przedstawia które dwie metody użytkownika służące do uwierzytelniania żądanie zresetowania hasła. |
| wynik |**Porzucone** — użytkownika uruchomiony resetowania hasła, ale został zatrzymany połowie, za pośrednictwem, przerywając<p>**Zablokowane** — konto użytkownika nie mógł używać resetowania z powodu próby hasła do strony resetowania hasła lub jednego hasła zresetować bramy zbyt wiele razy w okresie 24 godzin.<p>**Anulowane** — uruchomiona resetowania hasła użytkownika, ale następnie kliknięto przycisk Anuluj, aby anulować części sposób za pomocą sesji <p>**Skontaktować się z administratorem** — użytkownika wystąpił problem podczas jego sesji, które on nie można rozpoznać, więc użytkownik kliknął link "Skontaktuj się z administratorem" zamiast zakończenie przepływu zresetować hasła<p>**Nie powiodło się** — użytkownik nie mógł zresetować hasło, prawdopodobnie ponieważ użytkownik nie został skonfigurowany do używania funkcji (np. Brak licencji, Brak informacji uwierzytelniania hasła zarządzane lokalnego, ale zapisywania zwrotnego jest wyłączone).<p>**Pomyślnie** — resetowania hasła zakończyło się pomyślnie. |
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

## <a name="next-steps"></a>Następne kroki
Poniżej podano linki do wszystkich stron dokumentacji związanych z resetowaniem haseł w usłudze Azure AD:

* **Jesteś tutaj, ponieważ masz problemy z logowaniem?** Jeśli tak, [w tym miejscu opisano, jak zmienić i zresetować własne hasło](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
* [**Jak to działa**](active-directory-passwords-how-it-works.md) — poznaj informacje o sześciu różnych komponentach usługi i dowiedz się, jak działają
* [**Wprowadzenie** ](active-directory-passwords-getting-started.md) — Dowiedz się, jak umożliwić użytkownikom Resetowanie i zmienianie swoich haseł w chmurze lub lokalnie
* [**Dostosowanie**](active-directory-passwords-customize.md) — dowiedz się, jak dostosować wygląd, sposób działania i zachowanie usługi do potrzeb organizacji
* [**Najlepsze praktyki**](active-directory-passwords-best-practices.md) — dowiedz się, jak szybko wdrożyć i efektywnie zarządzać hasłami w organizacji
* [**Często zadawane pytania**](active-directory-passwords-faq.md) — uzyskaj odpowiedzi na często zadawane pytania
* [**Rozwiązywanie problemów**](active-directory-passwords-troubleshoot.md) — dowiedz się, jak szybko rozwiązywać problemy związane z usługą
* [**Dowiedz się więcej**](active-directory-passwords-learn-more.md) — zgłębiaj szczegóły techniczne dotyczące sposobu działania usługi
