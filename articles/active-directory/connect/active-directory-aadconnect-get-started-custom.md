---
title: 'Azure AD Connect: instalacja niestandardowa | Microsoft Docs'
description: "Ten dokument zawiera szczegóły dotyczące opcji niestandardowej instalacji hello Azure AD Connect. Użyj tych instrukcji tooinstall usługi Active Directory za pośrednictwem usługi Azure AD Connect."
services: active-directory
keywords: "co to jest program Azure AD Connect, instalowanie usługi Active Directory, wymagane składniki usługi Azure AD"
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 6d42fb79-d9cf-48da-8445-f482c4c536af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: c49724fab78c5a1688662043f69506fff6f82104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="custom-installation-of-azure-ad-connect"></a>Niestandardowa instalacja programu Azure AD Connect
Azure AD Connect **niestandardowych ustawień** jest używany, jeśli chcesz, dodatkowe opcje dotyczące instalacji hello. Jeśli masz wiele lasów, lub jeśli użytkownik chce tooconfigure opcjonalnych funkcji nie obejmuje instalacji ekspresowej hello jest używany. W przypadku gdy hello jest używany we wszystkich przypadkach [ **instalacji ekspresowej** ](active-directory-aadconnect-get-started-express.md) opcji nie spełnia z wdrożeniem lub topologią.

Przed rozpoczęciem instalowania Azure AD Connect, upewnij się, zbyt[Pobierz Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) i pełne hello wstępnymi opisane w temacie [Azure AD Connect: sprzęt i wymagania wstępne](active-directory-aadconnect-prerequisites.md). Sprawdź także, czy dostępne są wymagane konta, zgodnie z opisem w temacie [Konta i uprawnienia w programie Azure AD Connect](active-directory-aadconnect-accounts-permissions.md).

Dostosowane ustawienia niezgodna topologii, na przykład tooupgrade narzędzia DirSync, zobacz [dokumentację pokrewną](#related-documentation) w innych sytuacjach.

## <a name="custom-settings-installation-of-azure-ad-connect"></a>Instalacja programu Azure AD Connect z ustawieniami niestandardowymi
### <a name="express-settings"></a>Ustawienia ekspresowe
Na tej stronie, kliknij przycisk **Dostosuj** toostart instalację z ustawieniami niestandardowymi.

### <a name="install-required-components"></a>Instalacja wymaganych składników
Podczas instalowania usług synchronizacji hello hello sekcja konfiguracji opcjonalnej może pozostać niezaznaczone i Azure AD Connect konfiguruje wszystko automatycznie. Obejmuje to skonfigurowanie wystąpienia programu SQL Server 2012 Express LocalDB, tworzyć hello odpowiednich grup i przypisanie uprawnień. Jeśli chcesz toochange hello domyślne, można użyć hello następujące opcje konfiguracji opcjonalnej hello toounderstand tabeli, które są dostępne.

![Wymagane składniki](./media/active-directory-aadconnect-get-started-custom/requiredcomponents.png)

| Konfiguracja opcjonalna | Opis |
| --- | --- |
| Użyj istniejącego serwera SQL Server |Umożliwia toospecify programu SQL Server hello i nazwa wystąpienia hello. Wybierz tę opcję, jeśli masz już serwer bazy danych, które chcesz toouse. Wprowadź nazwę wystąpienia hello, a następnie przecinek i numer portu w **nazwa wystąpienia** Jeśli program SQL Server nie jest wyłączona funkcja przeglądania. |
| Użyj istniejącego konta usługi |Azure AD Connect używa domyślnie konta usług wirtualnych dla toouse usługi synchronizacji hello. Jeśli zdalnego programu SQL Server lub serwer proxy, który wymaga uwierzytelniania, należy toouse **zarządzane konto usługi** lub użyć konta usługi w domenie hello i o hello hasła. W takich przypadkach wprowadź hello toouse konta. Upewnij się, że hello użytkownika uruchamiającego instalację hello jest Skojarzenie w programie SQL, dlatego można utworzyć nazwy logowania dla konta usługi hello. Zobacz temat [Konta i uprawnienia w programie Azure AD Connect](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) |
| Określ niestandardowe grupy synchronizacji |Domyślnie Azure AD Connect tworzy cztery grupy lokalne toohello serwera podczas instalowania usług synchronizacji hello. Grupy te stanowią: grupy administratorów, grupa operatorów, grupa przeglądania i hello grupa Resetowanie hasła. Możesz tu określić własne grupy. grupy Hello musi określać elementy lokalne powitania serwera i nie może znajdować się w domenie hello. |

### <a name="user-sign-in"></a>Logowanie użytkowników
Po zainstalowaniu hello wymagane składniki, zostanie wyświetlona prośba tooselect użytkownikom pojedynczy metodę logowania jednokrotnego. w poniższej tabeli Hello zawiera krótki opis dostępnych opcji hello. Aby uzyskać pełny opis metod logowania hello, zobacz [logowania użytkownika](active-directory-aadconnect-user-signin.md).

![Logowanie użytkownika](./media/active-directory-aadconnect-get-started-custom/usersignin2.png)

| Opcja logowania jednokrotnego | Opis |
| --- | --- |
| Synchronizacja haseł |Użytkownicy będą mogli toosign tooMicrosoft usług w chmurze, takich jak Office 365 przy użyciu tego samego hasła, które używają w swoich sieciach lokalnych hello. Witaj hasła użytkowników są synchronizowane tooAzure AD jako skrót hasła, a uwierzytelnianie odbywa się w chmurze hello. Więcej informacji znajduje się w temacie [Synchronizacja haseł](active-directory-aadconnectsync-implement-password-synchronization.md). |
|Uwierzytelnianie przekazywane (wersja zapoznawcza)|Użytkownicy będą mogli toosign tooMicrosoft usług w chmurze, takich jak Office 365 przy użyciu tego samego hasła, które używają w swoich sieciach lokalnych hello.  hasła użytkowników Hello jest przekazywana toohello lokalnej usługi Active Directory kontrolera toobe zweryfikowany.
| Federacja z usługami AD FS |Użytkownicy będą mogli toosign tooMicrosoft usług w chmurze, takich jak Office 365 przy użyciu tego samego hasła, które używają w swoich sieciach lokalnych hello.  Witaj, użytkownicy są przekierowywani tootheir toosign wystąpienia usług AD FS w lokalnymi i uwierzytelnianie odbywa się lokalnie. |
| Nie konfiguruj |Żadna z funkcji nie jest zainstalowana ani skonfigurowana. Wybierz tę opcję, jeśli masz już serwer federacyjny innej firmy lub korzystasz z innego rozwiązania. |
|Włącz logowanie jednokrotne|Ta opcja jest dostępna z synchronizacji haseł i uwierzytelniania przekazywanego i zapewnia rejestracji jednokrotnej na środowisko pulpitu użytkownikom w sieci firmowej hello.  Aby uzyskać więcej informacji, zobacz [Logowanie jednokrotne](active-directory-aadconnect-sso.md). </br>Uwaga dla klientów usług AD FS ta opcja jest niedostępna, ponieważ usługi AD FS już tego samego poziomu hello oferty jednokrotne.</br>(jeśli PTA nie zostaje zwolniony na powitania jednocześnie)
|Opcja logowania|Ta opcja jest dostępna dla klientów synchronizacji haseł i zapewnia rejestracji jednokrotnej na środowisko pulpitu użytkownikom w sieci firmowej hello.  </br>Aby uzyskać więcej informacji, zobacz [Logowanie jednokrotne](active-directory-aadconnect-sso.md). </br>Uwaga dla klientów usług AD FS ta opcja jest niedostępna, ponieważ usługi AD FS już tego samego poziomu hello oferty jednokrotne.


### <a name="connect-tooazure-ad"></a>Połącz tooAzure AD
Na ekranie tooAzure AD Connect hello wprowadź nazwę i hasło konta administratora globalnego. W przypadku wybrania **Federacja z usługami AD FS** na poprzedniej stronie powitania, wystarczy nie rejestrować się za pomocą konta w domenie planujesz tooenable dla Federacji. Zalecenie jest toouse konta w domyślnej hello **onmicrosoft.com** domeny, który jest dostarczany z katalogiem Azure AD.

To konto jest tylko toocreate używane konto usługi w usłudze Azure AD i nie jest używany po zakończeniu hello kreatora.  
![Logowanie użytkownika](./media/active-directory-aadconnect-get-started-custom/connectaad.png)

Jeśli Twoje konto administratora globalnego jest włączone uwierzytelnianie MFA, należy tooprovide hello hasło ponownie w hello menu podręcznym logowania i hello pełne żądanie uwierzytelniania MFA. Żądanie hello można obejmować podanie kodu weryfikacyjnego lub rozmowę telefoniczną.  
![Logowanie użytkownika w usłudze MFA](./media/active-directory-aadconnect-get-started-custom/connectaadmfa.png)

Witaj konta administratora globalnego może być również [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md) włączone.

Jeśli wystąpi błąd lub problemy z łącznością, zobacz [Rozwiązywanie problemów z łącznością](active-directory-aadconnect-troubleshoot-connectivity.md).

## <a name="pages-under-hello-section-sync"></a>Strony w sekcji hello synchronizacji

### <a name="connect-your-directories"></a>Podłączanie katalogów
tooyour tooconnect usług domenowych w usłudze Active Directory, Azure AD Connect potrzebuje hello Nazwa lasu i poświadczenia konta z wystarczającymi uprawnieniami.

![Podłączanie katalogu](./media/active-directory-aadconnect-get-started-custom/connectdir01.png)

Po wprowadzeniu nazwy lasu hello i klikając **Dodaj katalog**, wyskakującym oknie dialogowym zostanie wyświetlona i wyświetli monit o hello następujące opcje:

| Opcja | Opis |
| --- | --- |
| Użyj istniejącego konta | Wybierz tę opcję, jeśli chcesz, aby konto tooprovide istniejących usług AD DS toobe używane Azure AD Connect w przypadku łączenia toohello AD lasu podczas synchronizacji katalogów. Możesz wprowadzić hello domeny w formacie NetBios lub FQDN, tj. FABRIKAM\syncuser lub fabrikam.com\syncuser. To konto może być kontem zwykłego użytkownika, ponieważ wymaga tylko domyślnych uprawnień odczytu hello. Jednak w zależności od scenariusza, mogą być potrzebne większe uprawnienia. Więcej informacji znajduje się w temacie [Konta i uprawnienia w programie Azure AD Connect](active-directory-aadconnect-accounts-permissions.md#create-the-ad-ds-account). |
| Utwórz nowe konto | Wybierz tę opcję, jeśli chcesz, aby Kreator Azure AD Connect toocreate hello usług AD DS konta wymaganego przez program Azure AD Connect do połączenia toohello AD lasu podczas synchronizacji katalogów. Gdy ta opcja jest zaznaczona, wprowadź hello użytkownika i hasło dla konta administratora przedsiębiorstwa. Witaj konta administratora przedsiębiorstwa podane posłuży przy użyciu usługi Azure AD Connect hello toocreate kreatora wymagane konta usług AD DS. Możesz wprowadzić hello domeny w formacie NetBios lub FQDN, czyli FABRIKAM\administrator lub fabrikam.com\administrator. |

![Podłączanie katalogu](./media/active-directory-aadconnect-get-started-custom/connectdir02.png)


### <a name="azure-ad-sign-in-configuration"></a>Konfiguracja logowania się w usłudze Azure AD
Ta strona umożliwia domen UPN hello tooreview obecnych w lokalnych usług AD DS, które zostały zweryfikowane w usłudze Azure AD. Ta strona umożliwia również tooconfigure hello atrybutu toouse dla hello userPrincipalName.

![Niezweryfikowane domeny](./media/active-directory-aadconnect-get-started-custom/aadsigninconfig.png)  
Sprawdź wszystkie domeny z oznaczeniem **Nie dodano** lub **Nie zweryfikowano**. Upewnij się, że używane domeny zostały zweryfikowane w usłudze Azure AD. Po zweryfikowaniu domen, kliknij symbol Odśwież hello. Aby uzyskać więcej informacji, zobacz [dodać i zweryfikować domeny hello](../active-directory-add-domain.md)

**UserPrincipalName** -hello atrybut userPrincipalName jest hello używany podczas logowania się w tooAzure AD i Office 365. Witaj domen używane, znanej także jako hello sufiks nazwy UPN, należy zweryfikować w usłudze Azure AD przed hello użytkowników są synchronizowane. Firma Microsoft zaleca tookeep hello domyślnego atrybutu userPrincipalName. Jeśli ten atrybut jest nierutowalny i nie można zweryfikować, a następnie jest możliwe tooselect innego atrybutu. Można na przykład wybrać adres e-mail jako atrybut hello zawierający hello identyfikator logowania. Użycie atrybutu innego niż userPrincipalName jest określane jako **alternatywny identyfikator**. Witaj wartość atrybutu alternatywnego Identyfikatora musi występować po hello RFC822 standardowa. Alternatywny identyfikator może być używany w przypadku synchronizacji haseł i federacji.

>[!NOTE]
> Po włączeniu uwierzytelniania przekazywanego musi mieć co najmniej jedną domenę zweryfikowaną w kolejności toocontinue za pomocą Kreatora hello.

> [!WARNING]
> Korzystanie z alternatywnego identyfikatora nie jest zgodne ze wszystkimi zadaniami usługi Office 365. Aby uzyskać więcej informacji, zobacz zbyt[Konfigurowanie alternatywnego Identyfikatora logowania](https://technet.microsoft.com/library/dn659436.aspx).
>
>

### <a name="domain-and-ou-filtering"></a>Filtrowanie domen i jednostek organizacyjnych
Domyślnie wszystkie domeny i jednostki organizacyjne są zsynchronizowane. Jeśli istnieją jakieś domeny lub jednostki organizacyjne, nie ma toosynchronize tooAzure AD, możesz usunąć zaznaczenie tych domen i jednostek organizacyjnych.  
![Filtrowanie domen i jednostek organizacyjnych](./media/active-directory-aadconnect-get-started-custom/domainoufiltering.png)  
Ta strona kreatora hello konfiguruje filtrowanie oparte na domenie, a oparte na jednostce Organizacyjnej. Jeżeli planujesz toomake zmian, zobacz [filtrowanie oparte na domenie](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) i [filtrowanie na podstawie jednostki organizacyjnej](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) przed wprowadzeniem tych zmian. Niektóre jednostki organizacyjne są istotne dla funkcji hello i nie powinno być niezaznaczone.

Jeśli używasz filtrowania opartego na jednostce organizacyjnej z programem Azure AD Connect w wersji wcześniejszej niż 1.1.524.0, nowe jednostki organizacyjne dodane później są domyślnie synchronizowane. Zachowanie hello to nowe jednostki organizacyjne nie mają być synchronizowane, a następnie można skonfigurować go po zakończeniu Kreatora hello z [filtrowanie na podstawie jednostki organizacyjnej](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering). Azure AD Connect wersji 1.1.524.0 lub po można wskazuje, czy nowe toobe jednostek organizacyjnych synchronizowane lub nie.

Jeśli planujesz toouse [filtrowanie na podstawie grupy](#sync-filtering-based-on-groups), następnie upewnij się, hello jednostki Organizacyjnej z grupą hello jest włączone i nie są filtrowane z filtrowania jednostki Organizacyjnej. Filtrowanie oparte na jednostce organizacyjnej jest stosowane przed filtrowaniem opartym na grupie.

Istnieje również możliwość, że niektóre domeny są niedostępne ze względu na ograniczenia toofirewall. Te domeny są domyślnie niezaznaczone i wyświetlane jest dla nich ostrzeżenie.  
![Niedostępne domeny](./media/active-directory-aadconnect-get-started-custom/unreachable.png)  
Jeśli to ostrzeżenie jest wyświetlane, upewnij się, że te domeny są rzeczywiście niedostępne i ostrzeżenie hello jest oczekiwane.

### <a name="uniquely-identifying-your-users"></a>Unikatowa identyfikacja użytkowników

#### <a name="select-how-users-should-be-identified-in-your-on-premises-directories"></a>Wybieranie sposobu identyfikowania użytkowników w katalogach lokalnych
Witaj funkcja dopasowywania w lasach umożliwia toodefine, w jaki sposób użytkownicy z lasów usługi AD DS są reprezentowane w usłudze Azure AD. Użytkownik może być wyświetlany tylko jeden raz we wszystkich lasach lub mieć kombinację włączonych i wyłączonych kont. Użytkownik Hello również może być reprezentowany jako kontakt w niektórych lasach.

![Unikatowe](./media/active-directory-aadconnect-get-started-custom/unique.png)

| Ustawienie | Opis |
| --- | --- |
| [Obsługiwani użytkownicy są reprezentowani jednokrotnie we wszystkich lasach](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Wszyscy użytkownicy są utworzeni jako pojedyncze obiekty w usłudze Azure AD. Witaj obiekty nie są łączone w magazynie metaverse hello. |
| [Atrybut poczty](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Ta opcja łączy użytkowników i kontaktów, jeśli atrybut poczty hello ma hello samą wartość w różnych lasach. Tej opcji należy użyć w przypadku, gdy kontakty zostały utworzone przy użyciu usługi GALSync. Jeśli zostanie wybrana ta opcja, obiektów użytkowników, których atrybut poczty nie są wypełnione nie będą synchronizowane tooAzure AD. |
| [Atrybuty ObjectSID i msExchangeMasterAccountSID/msRTCSIP-OriginatorSid](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Ta opcja łączy włączonego użytkownika w lesie konta z wyłączonym użytkownikiem w lesie zasobów. W programie Exchange ta konfiguracja jest określana jako połączona skrzynka pocztowa. Również można użyć tej opcji, jeśli używasz tylko Lync i programu Exchange nie jest obecny w lesie zasobów hello. |
| Atrybuty sAMAccountName i MailNickName |Ta opcja łączy atrybuty, których jest oczekiwany hello Identyfikatora logowania dla użytkownika hello można znaleźć. |
| Określony atrybut |Ta opcja umożliwia tooselect własnego atrybutu. Jeśli zostanie wybrana ta opcja, obiektów użytkowników, których atrybut (wybrane) nie są wypełnione nie będą synchronizowane tooAzure AD. **Ograniczenie:** upewnij się, że toopick atrybut, który znajduje się już w magazynie metaverse hello. W przypadku wybrania atrybutu niestandardowego (nie w hello metaverse) nie może ukończyć kreatora hello. |

#### <a name="select-how-users-should-be-identified-with-azure-ad---source-anchor"></a>Wybieranie sposobu identyfikowania użytkowników z usługą Azure AD — zakotwiczenie źródła
Witaj atrybut sourceAnchor jest atrybut, który jest niezmienialny w okresie istnienia hello obiektu użytkownika. Jest hello kluczem podstawowym łączącym użytkownika lokalnego hello hello użytkownika w usłudze Azure AD.

| Ustawienie | Opis |
| --- | --- |
| Let Zarządzanie zakotwiczenie źródła hello Azure | Wybierz tę opcję, jeśli ma atrybut hello toopick usługi Azure AD dla Ciebie. Jeśli wybierzesz tę opcję, Kreator Azure AD Connect stosuje hello sourceAnchor atrybut wyboru logiki opisane w sekcji artykułu [Azure AD Connect: zagadnienia dotyczące — przy użyciu msDS-ConsistencyGuid jako sourceAnchor projektowania](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). Kreator Hello informuje atrybut, którego została pobrana jako atrybut zakotwiczenia źródła powitania po zakończeniu instalacji niestandardowej. |
| Określony atrybut | Wybierz tę opcję, jeśli chcesz toospecify istniejący atrybut AD jako atrybut sourceAnchor hello. |

Ponieważ nie można zmienić atrybutu hello, należy zaplanować toouse właściwego atrybutu. Dobrym wyborem jest atrybut objectGUID. Ten atrybut nie zostanie zmieniona, chyba że hello konto użytkownika jest przenoszone między lasami/domenami. W środowisku wielu lasów, w którym konta są przenoszone między lasami inny atrybut musi być używany, np. atrybutu z hello identyfikator pracownika. Należy unikać atrybutów, które mogą ulec zmianie po zmianie stanu cywilnego lub zmianie zadań. Nie można używać atrybutów ze znakiem @-sign, więc nie można używać adresu e-mail ani atrybutu userPrincipalName. Atrybut Hello jest również wielkość liter podczas przenoszenia obiektu między lasami, upewnij się, że toopreserve hello wielkich/małych liter. Atrybuty binarne są zakodowane przy użyciu standardu base64, ale inne typy atrybutów pozostają w stanie niezakodowanym. W scenariuszach federacji i niektórych interfejsach usługi Azure AD ten atrybut nosi również nazwę immutableID. Więcej informacji na temat zakotwiczenia źródła hello znajdują się w hello [zagadnienia dotyczące projektowania](active-directory-aadconnect-design-concepts.md#sourceanchor).

### <a name="sync-filtering-based-on-groups"></a>Filtrowanie synchronizacji na podstawie grup
Witaj, funkcja filtrowania grup umożliwia toosync małego podzbioru obiektów do pilotażu. toouse tej funkcji, utworzyć grupę w tym celu w lokalnej usługi Active Directory. Następnie należy dodać użytkowników i grup, które mają zostać zsynchronizowane tooAzure AD jako bezpośrednie elementy członkowskie. Później można dodawać i usuwać użytkowników toothis grupy toomaintain hello listę obiektów, które powinny znajdować się w usłudze Azure AD. Wszystkie obiekty, które mają toosynchronize musi być bezpośrednimi elementami członkowskimi grupy hello. Wszyscy użytkownicy i wszystkie grupy, kontakty, komputery/urządzenia muszą być bezpośrednimi elementami członkowskimi. Członkostwo grup zagnieżdżonych nie jest rozpoznawane. Po dodaniu grupy po dodaniu elementu członkowskiego, tylko sama grupa hello, a nie jej elementy członkowskie.

![Filtrowanie synchronizacji](./media/active-directory-aadconnect-get-started-custom/filter2.png)

> [!WARNING]
> Ta funkcja jest tylko zamierzonego toosupport wdrożenia pilotażowego. Nie należy jej używać w pełnej wersji środowiska produkcyjnego.
>
>

W pełnej wersji środowiska produkcyjnego będzie toomaintain twardych toobe jedną grupę ze wszystkich toosynchronize obiektów. Zamiast tego należy użyć jednej z metod hello w [Konfigurowanie filtrowania](active-directory-aadconnectsync-configure-filtering.md).

### <a name="optional-features"></a>Funkcje opcjonalne
Ten ekran umożliwia tooselect hello funkcje opcjonalne dla określonych scenariuszy.

![Funkcje opcjonalne](./media/active-directory-aadconnect-get-started-custom/optional.png)

> [!WARNING]
> Jeśli masz obecnie narzędzia DirSync i Azure AD Sync active, nie należy aktywować żadnych funkcji zapisywania zwrotnego hello w programie Azure AD Connect.
>
>

| Funkcje opcjonalne | Opis |
| --- | --- |
| Wdrożenie hybrydowe programu Exchange |Hello funkcja wdrożenia hybrydowego programu Exchange umożliwia jednoczesne istnienie skrzynek pocztowych programu Exchange, hello lokalnie i w usłudze Office 365. Program Azure AD Connect synchronizuje określony zbiór [atrybutów](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) z usługi Azure AD z katalogiem lokalnym. |
| Foldery publiczne poczty programu Exchange | Funkcja folderów publicznych poczty programu Exchange Hello pozwala toosynchronize obsługujące pocztę folderu publicznego obiektów z sieci lokalnej usługi Active Directory tooAzure AD. |
| Filtrowanie atrybutów i aplikacji usługi Azure AD |Przez włączenie filtrowanie atrybutów i aplikacji usługi Azure AD, hello zsynchronizowanych atrybutów umożliwia dostosowanie zestawu. Ta opcja dodaje dwa więcej kreatora toohello strony konfiguracji. Więcej informacji znajduje się w temacie [Filtrowanie atrybutów i aplikacji usługi Azure AD](#azure-ad-app-and-attribute-filtering). |
| Synchronizacja haseł |Wybrano federacyjnego hello logowania rozwiązania, można włączyć tę opcję. Synchronizacja haseł może być następnie użyta jako opcja tworzenia kopii zapasowych. Dodatkowe informacje znajdują się w temacie [Synchronizacja haseł](active-directory-aadconnectsync-implement-password-synchronization.md). </br></br>W przypadku wybrania uwierzytelniania przekazywanego ta opcja jest włączona obsługa tooensure domyślne dla starszych klientów i jako opcji tworzenia kopii zapasowej. Dodatkowe informacje znajdują się w temacie [Synchronizacja haseł](active-directory-aadconnectsync-implement-password-synchronization.md).|
| Zapisywanie zwrotne haseł |Po włączeniu funkcji zapisywania zwrotnego haseł, zmiany wprowadzane w usłudze Azure AD są zapisywane tooyour katalogu lokalnego. Więcej informacji można znaleźć w temacie [Wprowadzenie do zarządzania hasłami](../active-directory-passwords-getting-started.md) |
| Zapisywanie zwrotne grup |Jeśli używasz hello **grupy usługi Office 365** funkcji mogą mieć tych grup reprezentowane w lokalnej usługi Active Directory. Ta opcja jest dostępna tylko, jeśli w lokalnej usłudze Active Directory jest dostępny program Exchange. Więcej informacji znajduje się w temacie [Zapisywanie zwrotne grup](active-directory-aadconnect-feature-preview.md#group-writeback). |
| Zapisywanie zwrotne urządzeń |Umożliwia toowriteback obiekty urządzeń w usłudze Azure AD tooyour lokalnej usługi Active Directory dla scenariuszy dostępu warunkowego. Więcej informacji znajduje się w temacie [Włączanie zapisywania zwrotnego urządzeń w programie Azure AD Connect](active-directory-aadconnect-feature-device-writeback.md). |
| Synchronizacja atrybutów rozszerzeń katalogów |Po włączeniu synchronizacji atrybutów rozszerzeń katalogów, określone atrybuty są zsynchronizowane tooAzure AD. Więcej informacji znajduje się w temacie [Rozszerzenia katalogów](active-directory-aadconnectsync-feature-directory-extensions.md). |

### <a name="azure-ad-app-and-attribute-filtering"></a>Filtrowanie atrybutów i aplikacji usługi Azure AD
Jeśli chcesz toolimit, które tooAzure toosynchronize atrybutów AD, należy najpierw wybrać usługi, które są używane. Jeśli wprowadzisz zmiany w konfiguracji na tej stronie, Nowa usługa ma toobe wybrać jawnie przez ponowne uruchomienie Kreatora instalacji hello.

![Funkcje opcjonalne — aplikacje](./media/active-directory-aadconnect-get-started-custom/azureadapps2.png)

Na podstawie hello usług wybrane w poprzednim kroku hello, ta strona zawiera wszystkie atrybuty, które są synchronizowane. Ta lista zawiera kombinację wszystkich typów obiektów, które są synchronizowane. Jeśli istnieją jakieś określone atrybuty, które należy toonot synchronizować, możesz usunąć zaznaczenie tych atrybutów.

![Funkcje opcjonalne — atrybuty](./media/active-directory-aadconnect-get-started-custom/azureadattributes2.png)

> [!WARNING]
> Usuwanie atrybutów może mieć wpływ na funkcjonalność. Aby poznać najlepsze rozwiązania i zalecenia, zobacz temat [Synchronizowane atrybuty](active-directory-aadconnectsync-attributes-synchronized.md#attributes-to-synchronize).
>
>

### <a name="directory-extension-attribute-sync"></a>Synchronizacja atrybutów rozszerzeń katalogów
Można rozszerzyć schemat hello w usłudze Azure AD o atrybuty niestandardowe dodane przez organizację użytkownika lub inne atrybuty w usłudze Active Directory. toouse tej funkcji, wybierz opcję **synchronizacja atrybutów rozszerzeń katalogu** na powitania **funkcje opcjonalne** strony. Można wybrać więcej atrybutów toosync na tej stronie.

![Rozszerzenia katalogów](./media/active-directory-aadconnect-get-started-custom/extension2.png)

Więcej informacji znajduje się w temacie [Rozszerzenia katalogów](active-directory-aadconnectsync-feature-directory-extensions.md).

### <a name="enabling-single-sign-on-sso"></a>Włączanie logowania jednokrotnego
Konfigurowanie rejestracji jednokrotnej do użytku z synchronizacji haseł lub przekazywanego uwierzytelniania jest prosty proces, że wystarczy tylko toocomplete raz dla każdego lasu, które są synchronizowane tooAzure AD. Konfiguracja obejmuje następujące dwa kroki:

1.  Utworzyć konto komputera niezbędne hello w lokalnej usługi Active Directory.
2.  Konfigurowanie strefy intranet hello komputerów klienckich hello toosupport pojedynczego logowania.

#### <a name="create-hello-computer-account-in-active-directory"></a>Tworzenie hello konta komputera w usłudze Active Directory
Dla każdego lasu, który został dodany w programie Azure AD Connect konieczne będzie toosupply poświadczenia administratora domeny, aby konto komputera hello można utworzyć w każdym lesie. Hello poświadczenia są tylko używane toocreate hello konta i są nie przechowywane lub używane dla innych operacji. Po prostu Dodaj hello poświadczeń na powitania **włączyć pojedynczego logowania** hello Azure AD Connect kreatora pokazany:

![Włączanie logowania jednokrotnego](./media/active-directory-aadconnect-get-started-custom/enablesso.png)

>[!NOTE]
>Można pominąć określonego lasu, jeśli nie chcesz, aby toouse logowania jednokrotnego z tego lasu.

#### <a name="configure-hello-intranet-zone-for-client-machines"></a>Konfigurowanie strefy Intranet powitania dla komputerów klienckich
tooensure powitania klienta logowania automatycznie w intranecie hello strefy można muszą tooensure, że dwa adresy URL są częścią hello strefy intranetowej. Dzięki temu, że hello komputerze przyłączonym do domeny automatycznie wysyła tooAzure biletu Kerberos AD, gdy jest toohello połączonych sieci firmowej.
Na komputerze, na którym zainstalowano narzędzia do zarządzania zasadami grupy hello.

1.  Otwieranie hello narzędzi do zarządzania zasadami grupy
2.  Edytuj hello zasad grupy, który ma być zastosowany tooall użytkowników. Na przykład hello domyślne zasady domeny.
3.  Przejdź za**strony Panel\Security formantu użytkownika Konfiguracja komputera\Szablony administracyjne\Składniki systemu Windows\Internet Explorer\Internetowy** i wybierz **tooZone Lista przypisywanie lokacji** na powitania obrazu poniżej.
4.  Włącz hello zasady, a następnie wprowadź następujące dwa elementy w oknie dialogowym hello hello.

        Value: `https://autologon.microsoftazuread-sso.com`  
        Data: 1  
        Value: `https://aadg.windows.net.nsatc.net`  
        Data: 1

5.  Jego wygląd powinien być podobne toohello następujące czynności:  
![Strefy intranetowe](./media/active-directory-aadconnect-get-started-custom/sitezone.png)

6.  Dwa razy kliknij przycisk **OK**.

## <a name="configuring-federation-with-ad-fs"></a>Konfigurowanie federacji przy użyciu usług AD FS
Konfigurowanie usług AD FS przy użyciu programu Azure AD Connect jest proste — wystarczy kilka kliknięć. następujące Hello jest wymagane przed hello konfiguracji.

* Serwer Windows Server 2012 R2 na powitania serwera federacyjnego z włączonym zarządzaniem zdalnym
* Serwer Windows Server 2012 R2 dla serwera Proxy aplikacji sieci Web hello z włączonym zarządzaniem zdalnym
* Certyfikat SSL dla Federacji hello usługi nazwa, która ma toouse (np. sts.contoso.com)

### <a name="ad-fs-configuration-pre-requisites"></a>Wymagania wstępne konfiguracji usług AD FS
tooconfigure usługi AD FS farmy, za pomocą usługi Azure AD Connect, upewnij się, na serwerach zdalnych hello jest włączona usługa WinRM. Ponadto przejść przez wymaganie porty hello na liście [tabela 3 - Azure AD Connect i serwery federacyjne/WAP](active-directory-aadconnect-ports.md#table-3---azure-ad-connect-and-ad-fs-federation-serverswap).

### <a name="create-a-new-ad-fs-farm-or-use-an-existing-ad-fs-farm"></a>Tworzenie nowej famy usług AD FS lub korzystanie z istniejącej farmy usług AD FS
Można użyć istniejącej farmy usług AD FS lub możesz wybrać toocreate nowej farmy usług AD FS. Jeśli toocreate wybrać nowe hasło, to certyfikat SSL hello tooprovide wymagane. Jeśli certyfikat SSL hello jest chroniony hasłem, zostanie wyświetlony monit o hasło hello.

![Farma usług AD FS](./media/active-directory-aadconnect-get-started-custom/adfs1.png)

Jeśli wybierzesz toouse istniejącej farmy usług AD FS, nastąpi bezpośrednio toohello Konfigurowanie hello relacji zaufania między ekranu usług AD FS a usługą Azure AD.

### <a name="specify-hello-ad-fs-servers"></a>Określ serwery hello usług AD FS
Wprowadź hello serwerów, które ma być tooinstall usług AD FS. Można dodać jeden serwer lub większą ich liczbę w zależności od tego, jakie są potrzeby związane z planowaniem wydajności. Dołącz do wszystkich serwerów tooActive katalogu, przed wykonaniem tej konfiguracji. Firma Microsoft zaleca instalowanie jednego serwera usług AD FS do celów wdrożeń testowych i pilotażowych. Następnie należy dodać i wdrożyć więcej serwerów toomeet potrzeb skalowania, uruchamiając ponownie po wykonaniu konfiguracji początkowej Azure AD Connect.

> [!NOTE]
> Upewnij się, czy wszystkie serwery są połączone tooan AD domeny przed wykonaniem tej konfiguracji.
>
>

![Serwery usług AD FS](./media/active-directory-aadconnect-get-started-custom/adfs2.png)

### <a name="specify-hello-web-application-proxy-servers"></a>Określ serwer Proxy aplikacji sieci Web hello
Wprowadź hello serwerów, które mają służyć jako serwer proxy aplikacji sieci Web. Serwer proxy aplikacji sieci web Hello jest wdrożony w sieci Obwodowej (sieć ekstranet) i obsługuje żądania uwierzytelniania z ekstranetu hello. Można dodać jeden serwer lub większą ich liczbę w zależności od tego, jakie są potrzeby związane z planowaniem wydajności. Firma Microsoft zaleca instalowanie jednego serwera proxy aplikacji sieci Web do celów wdrożeń testowych i pilotażowych. Następnie należy dodać i wdrożyć więcej serwerów toomeet potrzeb skalowania, uruchamiając ponownie po wykonaniu konfiguracji początkowej Azure AD Connect. Firma Microsoft zaleca mających równoważną liczbę uwierzytelniania toosatisfy serwerów proxy z sieci intranet hello.

> [!NOTE]
> <li> Jeśli hello konto, którego używasz nie jest administratorem lokalnym na serwerach hello usług AD FS, następnie zostanie wyświetlony monit o poświadczenia administratora.</li>
> <li> Upewnij się, że istnieje połączenie HTTP/HTTPS między hello Azure AD Connect serwera i serwera Proxy aplikacji sieci Web hello przed uruchomieniem tego kroku.</li>
> <li> Upewnij się, że istnieje połączenie HTTP/HTTPS między hello serwera aplikacji sieci Web i hello AD FS serwera tooallow uwierzytelniania żądań tooflow za pośrednictwem.</li>
>

![Aplikacja sieci Web](./media/active-directory-aadconnect-get-started-custom/adfs3.png)

Jesteś tooenter zostanie wyświetlony monit o poświadczenia, dzięki czemu hello serwera aplikacji sieci web można ustanowić bezpiecznego połączenia toohello AD FS serwer. Wymagane są poświadczenia administratora lokalnego na powitania serwera usług AD FS toobe.

![Serwer proxy](./media/active-directory-aadconnect-get-started-custom/adfs4.png)

### <a name="specify-hello-service-account-for-hello-ad-fs-service"></a>Określ konto usługi hello hello usług AD FS
Witaj AD FS usługi wymaga domeny usługi konta tooauthenticate użytkowników i sprawdzania informacji o użytkownikach w usłudze Active Directory. Obsługiwane są dwa typy kont usługi:

* **Konto usługi zarządzane przez grupę** — wprowadzone w usługach Active Directory Domain Services w systemie Windows Server 2012. Ten typ konta zapewnia usług, takich jak usługi AD FS, pojedyncze konto bez konieczności hasło konta hello tooupdate regularnie. Użyj tej opcji, jeśli masz już kontrolery domeny systemu Windows Server 2012 w domenie hello, do której należą serwery usług AD FS.
* **Konto użytkownika domeny** — ten typ konta wymaga tooprovide hasła i regularnie aktualizacji hello hasła podczas hello zmiany lub wygaśnięcia. Użyj tej opcji tylko wtedy, gdy nie ma kontrolerów domeny systemu Windows Server 2012 w domenie hello, do której należą serwery usług AD FS.

Jeśli zostało wybrane konto usługi zarządzane przez grupę i funkcja ta nie była nigdy używana w usłudze Active Directory, zostanie wyświetlony monit o poświadczenia administratora przedsiębiorstwa. Te poświadczenia są używane tooinitiate hello klucza magazynu i włączyć funkcję hello w usłudze Active Directory.

> [!NOTE]
> Jeśli hello AD FS usługi jest już zarejestrowany jako nazwę SPN w domenie hello, Azure AD Connect wykonuje toodetect wyboru.  Usługi AD DS nie zezwala na toobe zduplikowanej nazwy SPN zarejestrowanych na raz.  Jeśli zostanie znaleziony zduplikowanej nazwy SPN, nie będzie możliwe tooproceed dalsze do momentu usunięcia hello SPN.

![Konto usług AD FS](./media/active-directory-aadconnect-get-started-custom/adfs5.png)

### <a name="select-hello-azure-ad-domain-that-you-wish-toofederate"></a>Wybierz domenę hello Azure AD, że chcesz toofederate
Ta konfiguracja jest używane toosetup hello federacyjnej relacji między usług AD FS a usługą Azure AD. Umożliwia skonfigurowanie usług AD FS tooissue zabezpieczeń tokeny tooAzure AD, a konfiguruje usługi Azure AD tootrust hello tokenów z tego określonego wystąpienia usług AD FS. Ta strona umożliwia tylko tooconfigure jednej domenie w hello początkowej instalacji. Później można skonfigurować więcej domen przez ponowne uruchomienie programu Azure AD Connect.

![Domena usługi Azure AD](./media/active-directory-aadconnect-get-started-custom/adfs6.png)

### <a name="verify-hello-azure-ad-domain-selected-for-federation"></a>Sprawdź domeny hello Azure AD wybranej do Federacji
Po wybraniu hello toobe domeny federacyjnej Azure AD Connect dostarcza niezbędne informacje tooverify niezweryfikowanej domeny. Zobacz [Dodaj i sprawdź domeny hello](../active-directory-add-domain.md) jak toouse te informacje.

![Domena usługi Azure AD](./media/active-directory-aadconnect-get-started-custom/verifyfeddomain.png)

> [!NOTE]
> AD Connect prób tooverify hello domeny podczas hello skonfiguruj etapu. Tooconfigure w przypadku kontynuowania bez dodania niezbędnych rekordów DNS hello, Kreator hello nie jest możliwe toocomplete hello konfiguracji.
>
>

## <a name="configure-and-verify-pages"></a>Konfigurowanie i weryfikowanie stron
Konfiguracja Hello odbywa się na tej stronie.

> [!NOTE]
> Przed kontynuowaniem instalacji po skonfigurowaniu federacji należy upewnić się, że skonfigurowano [rozpoznawanie nazw dla serwerów federacyjnych](active-directory-aadconnect-prerequisites.md#name-resolution-for-federation-servers).
>
>

![Gotowe tooconfigure](./media/active-directory-aadconnect-get-started-custom/readytoconfigure2.png)

### <a name="staging-mode"></a>Tryb przejściowy
Jest to możliwe toosetup nowego serwera synchronizacji równolegle z trybem przejściowym. Jest tylko obsługiwana toohave jeden serwer synchronizacji wykonujący Eksport tooone katalogu w chmurze hello. Ale jeśli chcesz, aby toomove z innego serwera, na przykład jeden uruchomione narzędzie DirSync, można włączyć usługi Azure AD Connect w tryb przejściowy. Po włączeniu synchronizacji hello aparat importu i synchronizuje dane w zwykły, ale nie eksportuje żadnych elementów tooAzure AD lub AD. Witaj funkcje synchronizacji i hasła funkcji zapisywania zwrotnego haseł są wyłączone w trybie przejściowym.

![Tryb przejściowy](./media/active-directory-aadconnect-get-started-custom/stagingmode.png)

W trybie przejściowym, jest aparatu synchronizacji toohello wymagane zmiany można toomake i sprawdź, co się toobe wyeksportowane. Gdy hello Konfiguracja wygląda dobrze, uruchom ponownie Kreatora instalacji hello i Wyłącz tryb przejściowy. Dane są teraz wyeksportowanego tooAzure AD z tego serwera. Upewnij się, że toodisable hello innego serwera na powitania, które aktywnie eksportował na tym samym serwerze czasu tak tylko jeden.

Więcej informacji znajduje się w temacie [Tryb przejściowy](active-directory-aadconnectsync-operations.md#staging-mode).

### <a name="verify-your-federation-configuration"></a>Weryfikowanie konfiguracji federacji
Azure AD Connect sprawdza ustawienia DNS powitania po kliknięciu przycisku Weryfikuj hello.

**Sprawdzanie łączności z intranetem**

* Rozwiązywanie federacyjnego FQDN: Azure AD Connect sprawdza, czy federacyjnego hello nazwy FQDN można rozwiązać przez połączenie tooensure DNS. Azure AD Connect nie może rozpoznać hello nazwy FQDN, hello weryfikacja zakończy się niepowodzeniem. Upewnij się, że rekord DNS znajduje się w usłudze federacyjnej hello nazwy FQDN w kolejności toosuccessfully hello ukończenia weryfikacji.
* Rekord A systemu DNS: program Azure AD Connect sprawdza, czy istnieje rekord A dla usługi federacyjnej. W przypadku braku hello rekord A hello weryfikacja zakończy się niepowodzeniem. Utwórz A rekordu, a nie rekordu CNAME dla nazwy FQDN federacyjnym w kolejności toosuccessfully ukończyć powitalnych weryfikację.

**Sprawdzanie łączności z ekstranetem**

* Rozwiązywanie federacyjnego FQDN: Azure AD Connect sprawdza, czy federacyjnego hello nazwy FQDN można rozwiązać przez połączenie tooensure DNS.

![Zakończ](./media/active-directory-aadconnect-get-started-custom/completed.png)

![Weryfikuj](./media/active-directory-aadconnect-get-started-custom/adfs7.png)

Ponadto należy wykonać następujące kroki weryfikacji hello:

* Zweryfikuj, że możesz zalogować się w przeglądarce na komputerze dołączonym do domeny w intranecie hello: Podłącz toohttps://myapps.microsoft.com i sprawdź hello logowanie na zalogowanym koncie. konto administratora Hello wbudowanych AD DS nie są zsynchronizowane i nie może zostać użyta do weryfikacji.
* Zweryfikuj, że możesz zalogować się na urządzeniu hello ekstranetu. Na komputera domowego lub urządzenia przenośnego Połącz toohttps://myapps.microsoft.com i podanie poświadczeń.
* Sprawdź poprawność logowania wzbogaconego klienta. Połącz toohttps://testconnectivity.microsoft.com, wybierz hello **usługi Office 365** i wybierz opcję hello **Office 365 pojedynczy znak na Test**.

## <a name="next-steps"></a>Następne kroki
Po ukończeniu instalacji hello, wyloguj się i zaloguj ponownie tooWindows przed użyciem narzędzia Synchronization Service Manager lub Synchronization Rule Editor.

Teraz, gdy masz Azure AD Connect można [zweryfikować hello instalację i przypisywanie licencji](active-directory-aadconnect-whats-next.md).

Dowiedz się więcej o tych funkcjach, włączonych instalacji hello: [Zapobieganie przypadkowemu usuwaniu](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) i [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Dowiedz się więcej na te popularne tematy: [harmonogram i sposób synchronizacji tootrigger](active-directory-aadconnectsync-feature-scheduler.md).

Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
