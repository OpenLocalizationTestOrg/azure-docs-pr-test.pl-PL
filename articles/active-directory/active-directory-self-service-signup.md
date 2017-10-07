---
title: "aaaWhat jest rejestracja samoobsługowa na platformie Azure? | Microsoft Docs"
description: "Subskrypcji samoobsługowej — omówienie dla platformy Azure, jak toomanage hello procesu zakładania i jak tootake nazwy domeny DNS."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: b9f01876-29d1-4ab8-8b74-04d43d532f4b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: dbf3b59e3807e98f7bf39f3d5591fcde01667323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-self-service-signup-for-azure"></a>Czym jest rejestracja samoobsługowa na platformie Azure?
W tym temacie opisano proces subskrypcji samoobsługowej hello i w jaki sposób tootake nazwy domeny DNS.  

## <a name="why-use-self-service-signup"></a>Dlaczego warto używać subskrypcji samoobsługowej?
* Get tooservices klientów, które mają szybszy.
* Utwórz opartych na poczcie e-mail oferty usługi.
* Tworzenie przepływów opartych na poczcie e-mail signup szybko Zezwalaj użytkownikom toocreate tożsamości za pomocą ich aliasów e-mail pracy łatwych do zapamiętania.
* Niezarządzane katalogów platformy Azure można uwzględnić w zarządzanych katalogi później i można użyć ponownie dla innych usług.

## <a name="terms-and-definitions"></a>— Warunki
* **Portal rejestracji**: jest to metoda hello za pomocą którego użytkownik tworzy konto w usłudze w chmurze i ma tożsamość automatycznie utworzone dla nich w usłudze Azure Active Directory (Azure AD), na podstawie ich domenę poczty e-mail.
* **Niezarządzane katalogu Azure**: to jest katalog hello miejsce tworzenia tej tożsamości. Niezarządzane katalog jest katalogiem, który nie ma administratora globalnego.
* **Zweryfikować adres e-mail użytkownika**: jest to typ konta użytkownika w usłudze Azure AD. Użytkownik, który ma tożsamość automatycznie utworzone po zarejestrowaniu się do oferty samoobsługi nazywa się zweryfikować adres e-mail użytkownika. Zweryfikować adres e-mail użytkownika jest członkiem regularne katalogu z creationmethod = EmailVerified.

## <a name="user-experience"></a>Środowisko użytkownika
Na przykład, załóżmy, że użytkownik, którego poczta e-mail jest Dan@BellowsCollege.com odbiera poufnych plików za pośrednictwem poczty e-mail. Witaj plików chronionych przez usługę Azure Rights Management (Azure RMS). Jednak organizacji Dan firmy, uczelni miech nie została podpisana dla usługi Azure RMS ani nie została wdrożona Active Directory RMS. W takim przypadku Dan można założyć tooRMS bezpłatnej subskrypcji dla osoby w kolejności tooread hello chronione pliki.

Jeśli Dan hello pierwszego użytkownika za pomocą adresu e-mail z toosign BellowsCollege.com dla tego samoobsługi oferty, następnie niezarządzane będzie można utworzyć katalogu dla BellowsCollege.com w usłudze Azure AD. Jeśli innym użytkownikom z domeny BellowsCollege.com hello Załóż tej oferty lub podobne oferty samoobsługi, będą miały również zweryfikować adres e-mail konta utworzone w hello sam niezarządzanych katalogu platformy Azure.

## <a name="admin-experience"></a>Środowisko pracy administratora
Administrator, który jest właścicielem nazwy domeny DNS hello niezarządzane katalogu Azure może przejąć lub scalania katalogu hello po potwierdzania własności. Witaj kolejnych sekcjach wyjaśniono środowisko pracy administratora hello bardziej szczegółowo, ale w tym miejscu znajduje się podsumowanie:

* Po przejęciu niezarządzane usługi Azure directory stają się po prostu hello administratorem globalnym katalogu niezarządzane hello. Jest to czasem nazywane przejęcia wewnętrznego.
* Podczas scalania niezarządzane katalogu platformy Azure, Dodaj nazwę domeny DNS hello zarządzanych katalogu Azure hello niezarządzane katalogu tooyour i mapowanie użytkowników do zasobów zostanie utworzony tak użytkownicy mogą nadal usług tooaccess bez przeszkód. Jest to czasem nazywane przejęcia zewnętrznych.

## <a name="what-gets-created-in-azure-active-directory"></a>Pobiera co utworzone w usłudze Azure Active Directory?
#### <a name="directory"></a>Katalog
* Katalog usługi Azure Active Directory dla domeny hello utworzeniu jednego katalogu dla domeny.
* katalog usługi Azure AD Hello ma nie administratora globalnego.

#### <a name="users"></a>Użytkownicy
* Dla każdego użytkownika, która zarejestruje się w katalogu usługi Azure AD hello tworzony jest obiekt użytkownika.
* Każdy obiekt użytkownika jest oznaczony jako zewnętrzny.
* Każdy użytkownik otrzymuje dostęp toohello usługi, która one podpisane w.

### <a name="how-do-i-claim-a-self-service-azure-ad-directory-for-a-domain-i-own"></a>Jak oświadczenia samoobsługi usługi Azure AD katalogu dla domeny własnym?
Samoobsługowe usługi Azure AD mogą rezerwować katalogu, wykonując weryfikacji domeny. Weryfikacji domeny potwierdza hello własnej domeny przez utworzenie rekordów DNS.

Istnieją dwa sposoby toodo przejęciem DNS katalogu usługi Azure AD:

* Przejmowanie wewnętrzne (Admin odnajduje niezarządzane katalogu platformy Azure i chce tooturn do katalogu zarządzane)
* zewnętrzne przejęcia (tooadd nowej domeny tootheir Azure katalogiem zarządzanym próbuje administratora)

Może Cię zainteresować sprawdzanie poprawności właścicielem domeny, ponieważ przejęcia niezarządzane katalogu po użytkownik wykona subskrypcji samoobsługowej, lub Dodawanie nowej domeny tooan istniejących zarządzanych katalogu. Na przykład masz domenę o nazwie contoso.com i ma tooadd nowej domeny o nazwie contoso.co.uk lub contoso.uk.

## <a name="what-is-domain-takeover"></a>Co to jest przejęcia domeny?
W tej sekcji opisano sposób toovalidate, że jesteś właścicielem domeny

### <a name="what-is-domain-validation-and-why-is-it-used"></a>Co to jest weryfikacji domeny i dlaczego służy?
Podczas operacji tooperform kolejności w katalogu usługi Azure AD wymaga sprawdzania poprawności prawa własności hello DNS domeny.  Weryfikacji domeny hello umożliwia możesz tooclaim hello katalogu i albo podwyższania poziomu hello samoobsługi katalogu tooa zarządzany katalog lub scalania hello samoobsługi katalogu do istniejącego zarządzane katalogu.

## <a name="examples-of-domain-validation"></a>Przykłady weryfikacji domeny
Istnieją dwa sposoby toodo przejęciem DNS katalogu:

* Przejmowanie wewnętrzne (na przykład administrator odnajduje samoobsługi katalogu niezarządzane i chce tooturn do katalogu zarządzane)
* przejęcia zewnętrznych (na przykład administrator próbuje tooadd nowy katalog zarządzanych tooa domeny)

### <a name="internal-takeover---promote-a-self-service-unmanaged-directory-toobe-a-managed-directory"></a>Wewnętrzny przejęcia - wspierania toobe samoobsługi, niezarządzany katalogu zarządzany katalog
Po wykonaniu wewnętrzny przejęcia katalogu hello zostaje przekształcona z katalogu zarządzanych tooa niezarządzane katalogu. Należy toocomplete DNS domeny sprawdzanie poprawności nazwy, gdzie utworzyć rekord MX lub rekord TXT w strefie DNS hello. Ta akcja:

* Sprawdza, czy jesteś właścicielem domeny hello
* Sprawia, że katalog hello zarządzane
* Sprawia, że hello administratora globalnego katalogu hello

Załóżmy, że administrator IT z uczelni miech wykrywa, czy użytkownicy z służbowe hello utworzyli konto samoobsługi oferty. Zarejestrowany hello BellowsCollege.com nazwa właściciela hello DNS, hello IT administrator może zweryfikować prawo własności nazwy DNS hello na platformie Azure, a następnie podjęcia za pośrednictwem katalogu niezarządzane hello. Witaj directory staje się zarządzany katalog, a hello administratora IT przypisano rolę administratora globalnego hello hello BellowsCollege.com katalogu.

### <a name="external-takeover---merge-a-self-service-directory-into-an-existing-managed-directory"></a>Zewnętrzne przejęcia - scalić samoobsługi katalogu do istniejącego katalogu zarządzanych
W zewnętrznej przejęcia masz już zarządzany katalog i mają wszyscy użytkownicy i grupy z toojoin niezarządzane katalogu, który zarządzany katalogu, a nie własnych dwa oddzielne katalogów.

Jako administrator katalogu zarządzanych Dodaj domeny i tej domeny sytuacji toohave niezarządzane katalog skojarzony z nim.

Na przykład załóżmy, że jesteś administratorem IT i już zarządzane katalogu dla domeny Contoso.com, nazwę domeny, która jest zarejestrowany tooyour organizacji. Użytkownik stwierdzi, że użytkownicy z organizacji wykonali samoobsługi logowania się oferty przy użyciu nazwy domeny poczty e-mail user@contoso.co.uk, która jest inną nazwę domeny, która własnością Twojej organizacji. Te użytkownicy mają obecnie konta w katalogu contoso.co.uk niezarządzane.

Nie chcesz toomanage dwa oddzielne katalogi, więc scalania hello niezarządzane katalogu contoso.co.uk z istniejącym katalogiem IT zarządzane dla domeny contoso.com.

Zewnętrzne sposób przejęcia hello tego samego procesu weryfikacji DNS jako przejęcia wewnętrznego.  Czym różnicę: Użytkownicy i usługi są ponownie zmapowany toohello IT zarządzany katalog.

#### <a name="whats-hello-impact-of-performing-an-external-takeover"></a>Jaki jest wpływ hello wykonania zewnętrznego przejęcia?
Z zewnętrznego przejęcia mapowanie użytkowników do zasobów jest tworzone użytkownicy mogą nadal usług tooaccess bez przeszkód. Wiele aplikacji, w tym usługi RMS dla użytkowników indywidualnych, również obsługiwać hello mapowanie użytkowników do zasobów, a użytkownicy mogą nadal tooaccess tych usług bez zmian. Jeśli aplikacja nie obsługuje skutecznie hello mapowanie użytkowników do zasobów, zewnętrznych przejęcia mogą być tooprevent jawnie zablokowanych użytkowników doświadczeniu niska.

#### <a name="directory-takeover-support-by-service"></a>Obsługa przejęcia Directory przez usługę
Obecnie powitania po przejęciu pomocy technicznej usługi:

* USŁUG RMS

przejęcia wkrótce będzie obsługiwana Hello następujące usługi:

* Usługa PowerBI

następujące Hello nie i wymaga administratora dodatkowych akcji toomigrate użytkownika danych po przejęciu zewnętrznych.

* SharePoint/OneDrive

## <a name="how-tooperform-a-dns-domain-name-takeover"></a>Jak tooperform domeny DNS nazwy przejęcia
Dostępnych jest kilka opcji jak tooperform weryfikacji domeny (i do przejęcia, w razie potrzeby):

1. Portal zarządzania systemu Azure

   Przejęciem jest wyzwalane, wykonując dodawania domeny.  Jeśli katalog już istnieje w domenie hello, będziesz mieć tooperform opcji hello przejęcia zewnętrznych.

   Zaloguj się toohello portalu Azure przy użyciu poświadczeń.  Przejdź tooyour istniejącym katalogiem, a następnie zbyt**Dodaj domenę**.
2. Office 365

   Można użyć opcji hello na powitania [Zarządzanie domenami](https://support.office.com/article/Navigate-to-the-Office-365-Manage-domains-page-026af1f2-0e6d-4f2d-9b33-fd147420fac2/) strony w toowork usługi Office 365 z domen i rekordów DNS. Zobacz [Sprawdź domenę, w usłudze Office 365](https://support.office.com/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611/).
3. Windows PowerShell

   Witaj następujące kroki są wymagane tooperform weryfikacji przy użyciu programu Windows PowerShell.

   | Krok | Polecenia cmdlet toouse |
   | --- | --- |
   | Utwórz obiekt poświadczeń |Get-Credential |
   | Połącz tooAzure AD |Connect-MsolService |
   | Pobierz listę domen |Get-MsolDomain |
   | Utwórz żądanie |Get-MsolDomainVerificationDns |
   | Utwórz rekord DNS |To zrobić na serwerze DNS |
   | Sprawdź hello żądania |Confirm-MsolEmailVerifiedDomain |

Na przykład:

1. Połącz tooAzure AD przy użyciu poświadczeń hello, które były używane toorespond toohello samoobsługi oferty:

        import-module MSOnline
        $msolcred = get-credential
        connect-msolservice -credential $msolcred
2. Pobierz listę domen:

    Get-MsolDomain
3. Następnie uruchom toocreate polecenia cmdlet Get-MsolDomainVerificationDns hello żądanie:

    Get-MsolDomainVerificationDns — DomainName *your_domain_name* — tryb DnsTxtRecord

    Na przykład:

    Get-MsolDomainVerificationDns — DomainName contoso.com — tryb DnsTxtRecord
4. Skopiuj wartość hello (hello challenge), która jest zwracana z tego polecenia.

    Na przykład:

    MS = 32DD01B82C05D27151EA9AE93C5890787F0E65D9
5. W sieci publicznej przestrzeni nazw DNS należy utworzyć rekord txt DNS, zawierający wartość hello, skopiowanego w poprzednim kroku hello.

    Hello nazwę dla tego rekordu jest nazwa domeny nadrzędnej hello Witaj, więc jeśli utworzysz ten rekord zasobu przy użyciu hello roli DNS z systemem Windows Server puste nazwy rekordu hello i wkleić tylko hello wartość w polu tekstowym hello
6. Uruchom hello Potwierdź MsolDomain polecenia cmdlet tooverify hello żądania:

    Potwierdź MsolEmailVerifiedDomain - DomainName *your_domain_name*

    Na przykład:

    Potwierdź MsolEmailVerifiedDomain - DomainName contoso.com

Żądanie powiodło się zwraca wiersz toohello bez błędów.

## <a name="how-do-i-control-self-service-settings"></a>Jak kontrolować ustawienia samoobsługowego?
Administratorzy mają dwa formanty samoobsługi dzisiaj. Kontrolować:

* Określa, czy użytkownicy mogą dołączać katalogu hello za pośrednictwem poczty e-mail.
* Określa, czy użytkownicy mogą licencji się dla aplikacji i usług.

### <a name="how-can-i-control-these-capabilities"></a>Metody kontrolowania tych funkcji
Administrator można skonfigurować te funkcje przy użyciu tych parametrów polecenia cmdlet Set-MsolCompanySettings usługi Azure AD:

* **AllowEmailVerifiedUsers** Określa, czy użytkownik może utworzyć czy Dołącz katalog niezarządzane. Jeśli wartość parametru zbyt$ false, nie weryfikacji wiadomości e-mail użytkownicy mogą dołączać hello katalogu.
* **AllowAdHocSubscriptions** kontroluje zdolność hello Zarejestruj tooperform samoobsługi użytkowników. Jeśli ten parametr zostanie ustawiona zbyt$ ma wartość FAŁSZ, użytkownicy nie mogą wykonywać subskrypcji samoobsługowej.

### <a name="how-do-hello-controls-work-together"></a>Jak formanty hello działają razem?
Te dwa parametry mogą być używane w połączeniu toodefine dokładniejszej kontroli nad samoobsługi Zarejestruj. Na przykład następujące polecenie hello umożliwi użytkowników tooperform samoobsługowego tworzenia konta, ale tylko wtedy, jeśli ci użytkownicy mają już konto w usłudze Azure AD (innymi słowy, użytkownicy potrzebują toobe zweryfikować adres e-mail konta tworzone nie można wykonać samoobsługi logowania się):

    Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true

Witaj poniższy schemat wyjaśniono wszystkich hello różnych kombinacji tych parametrów i warunki wynikowy hello hello katalogu i samoobsługowego tworzenia konta.

![][1]

Aby uzyskać więcej informacji i przykłady toouse tych parametrów, zobacz temat [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).

## <a name="see-also"></a>Zobacz też
* [Jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview)
* [Azure PowerShell](/powershell/azure/overview)
* [Dokumentacja poleceń cmdlet platformy Azure](/powershell/azure/get-started-azureps)
* [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)

<!--Image references-->
[1]: ./media/active-directory-self-service-signup/SelfServiceSignUpControls.png
