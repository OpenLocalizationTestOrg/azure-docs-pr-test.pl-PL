---
title: "aaaSetting lokalnego dostępu warunkowego przy użyciu rejestracji urządzeń usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Przewodnik krok po kroku tooenabling dostępu warunkowego lokalnego tooon aplikacji przy użyciu usługi Active Directory Federation Services (AD FS) w systemie Windows Server 2012 R2."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6ae9df8b-31fe-4d72-9181-cf50cfebbf05
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 808e3b96873102aebae667153f588dcdb205e884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-on-premises-conditional-access-by-using-azure-active-directory-device-registration"></a>Konfigurowanie lokalnego dostępu warunkowego przy użyciu rejestracji urządzeń usługi Azure Active Directory
Sprzężenia tooworkplace użytkownicy potrzebują ich urządzeń osobistych toohello usługi rejestracji urządzeń usługi Azure Active Directory (Azure AD), ich urządzeń może oznaczony jako znanych tooyour organizacji. Poniżej znajduje się przewodnik krok po kroku dotyczące włączania dostępu warunkowego lokalnego tooon aplikacji przy użyciu usługi Active Directory Federation Services (AD FS) w systemie Windows Server 2012 R2.

> [!NOTE]
> Licencja usługi Office 365 lub Azure AD Premium licencji jest wymagana podczas używania urządzenia, które są zarejestrowane w zasad dostępu warunkowego usługi rejestracji urządzeń usługi Azure Active Directory. Obejmują one zasady, których przestrzeganie jest wymuszane przez usługę AD FS w lokalnych zasobów.
> 
> Aby uzyskać więcej informacji na temat hello scenariuszy dostępu warunkowego dla zasobów lokalnych, zobacz [dołączanie tooworkplace z dowolnego urządzenia na potrzeby logowania jednokrotnego i łatwego uwierzytelniania dwuskładnikowego w aplikacjach firmy](https://technet.microsoft.com/library/dn280945.aspx).

Te funkcje są dostępne toocustomers, który zakupu licencji usługi Azure Active Directory Premium.

## <a name="supported-devices"></a>Obsługiwane urządzenia
* Urządzenia przyłączone do domeny systemu Windows 7
* Windows 8.1 urządzeń osobistych i przyłączonych do domeny
* iOS 6 i nowsze przeglądarki Safari hello
* System android 4.0 lub nowszy, Samsung GS3 lub telefony nowsze, Samsung Galaxy Uwaga 2 lub nowsze tabletów

## <a name="scenario-prerequisites"></a>Warunki wstępne scenariusza
* Subskrypcja tooOffice 365 lub Azure Active Directory Premium
* Dzierżawy usługi Azure Active Directory
* Windows Server Active Directory (Windows Server 2008 lub nowszy)
* Zaktualizowany schemat w systemie Windows Server 2012 R2
* Licencja usługi Azure Active Directory — wersja Premium
* Windows Server 2012 R2 usług federacyjnych, skonfigurowany do logowania jednokrotnego tooAzure AD
* Serwer Proxy aplikacji sieci Web systemu Windows Server 2012 R2 
* Microsoft Azure Active Directory Connect (Azure AD Connect) [(Pobieranie programu Azure AD Connect)](http://www.microsoft.com/en-us/download/details.aspx?id=47594)
* Zweryfikowanej domeny

## <a name="known-issues-in-this-release"></a>Znane problemy w tej wersji
* Zasady dostępu warunkowego opartego na urządzenia wymagają urządzenia obiektu zapisywania zwrotnego tooActive katalogu z usługą Azure Active Directory. Toothree godzin zapisywane tooActive katalogu toobe obiektów urządzenia może potrwać.
* urządzenia z systemem iOS 7 zawsze Monituj hello użytkownika tooselect certyfikatu podczas uwierzytelniania certyfikatu klienta.
* Niektóre wersje systemu iOS 8 przed iOS 8.3 nie działają.

## <a name="scenario-assumptions"></a>Założenia scenariusza
W tym scenariuszu założono, że środowisku hybrydowym, składające się z dzierżawy usługi Azure AD i lokalnej usługi Active Directory. Te dzierżaw powinny być połączone z programem Azure AD Connect, zweryfikowanej domeny i usług AD FS dla logowania jednokrotnego. Użyj następującej listy kontrolnej toohelp skonfigurować środowisko zgodnie z wymaganiami toohello hello.

## <a name="checklist-prerequisites-for-conditional-access-scenario"></a>Lista kontrolna: Wymagania wstępne dotyczące dla scenariuszy dostępu warunkowego
Połącz dzierżawy usługi Azure AD z lokalnym wystąpieniem usługi Active Directory.

## <a name="configure-azure-active-directory-device-registration-service"></a>Konfigurowanie usługi rejestracji urządzeń usługi Azure Active Directory
Użyj tego przewodnika toodeploy i skonfigurowanie usługi rejestracji urządzeń usługi Azure Active Directory hello w Twojej organizacji.

W tym przewodniku założono, że skonfigurowano usługi Active Directory systemu Windows Server, a masz subskrypcję usługi Azure Active Directory tooMicrosoft. Zobacz wymagania wstępne hello opisany wcześniej.

Witaj toodeploy usługi rejestracji urządzeń usługi Azure Active Directory z usługą Azure Active Directory dzierżawy hello ukończenia zadania w hello następującej listy kontrolnej w kolejności. Gdy łącze odwołania ma temat dotyczący pojęć tooa, zwracać toothis Lista kontrolna później, tak, aby móc kontynuować wykonywanie hello pozostałych zadań. Niektóre zadania obejmują krok weryfikacji scenariusz, który ułatwia upewnij się, czy krok hello została ukończona pomyślnie.

## <a name="part-1-enable-azure-active-directory-device-registration"></a>Część 1: Rejestracja urządzeń Włączanie usługi Azure Active Directory
Wykonaj kroki hello w tooenable Lista kontrolna hello i konfigurowanie usługi rejestracji urządzeń usługi Azure Active Directory hello.

| Zadanie | Dokumentacja | 
| --- | --- |
| Włączanie rejestracji urządzeń w miejscu pracy usługi Azure Active Directory dzierżawy tooallow urządzeń toojoin hello. Domyślnie usługa Azure Multi-Factor Authentication nie jest włączone dla usługi hello. Jednak zaleca się korzystanie z uwierzytelniania wieloskładnikowego podczas rejestrowania urządzenia. Przed włączeniem uwierzytelniania wieloskładnikowego w usłudze rejestracji w usłudze Active Directory, upewnij się, że usługi AD FS jest skonfigurowany dla dostawcy uwierzytelniania wieloskładnikowego. |[Włączanie rejestracji urządzeń usługi Azure Active Directory](active-directory-device-registration-get-started.md)| 
|Wykrywa urządzenia z usługi rejestracji urządzeń usługi Azure Active Directory przez wyszukiwanie dobrze znanych rekordów systemu DNS. System DNS firmy należy skonfigurować tak, aby urządzenia odnajdywania usługi rejestracji urządzeń usługi Azure Active Directory. |[Konfigurowanie odnajdywania rejestracji urządzeń usługi Azure Active Directory](active-directory-device-registration-get-started.md)| 


## <a name="part-2-deploy-and-configure-windows-server-2012-r2-active-directory-federation-services-and-set-up-a-federation-relationship-with-azure-ad"></a>Część 2: Wdróż i skonfiguruj Active Directory Federation Services do systemu Windows Server 2012 R2 i skonfiguruj relację federacji z usługą Azure AD

| Zadanie | Dokumentacja |
| --- | --- |
| Wdrażanie usług domenowych w usłudze Active Directory z rozszerzeniami schematu systemu Windows Server 2012 R2 hello. Nie trzeba tooupgrade żadnego z tooWindows kontrolery domeny Server 2012 R2. Uaktualnienie schematu Hello jest jedynym wymaganiem hello. |[Uaktualnienia schematu do usług domenowych w usłudze Active Directory](#upgrade-your-active-directory-domain-services-schema) |
| Wykrywa urządzenia z usługi rejestracji urządzeń usługi Azure Active Directory przez wyszukiwanie dobrze znanych rekordów systemu DNS. System DNS firmy należy skonfigurować tak, aby urządzenia odnajdywania usługi rejestracji urządzeń usługi Azure Active Directory. |[Przygotowywanie urządzenia pomocy technicznej usługi Active Directory](#prepare-your-active-directory-to-support-devices) |

## <a name="part-3-enable-device-writeback-in-azure-ad"></a>Część 3: Zapisywanie zwrotne urządzeń Włącz w usłudze Azure AD
| Zadanie | Dokumentacja |
| --- | --- |
| Zakończenie części "Włączanie zapisywania zwrotnego urządzeń w programie Azure AD Connect." Po zakończeniu jego przewodnik toothis zwracany. |[Włączanie zapisywania zwrotnego urządzeń w programie Azure AD Connect](#upgrade-your-active-directory-domain-services-schema) |

## <a name="optional-part-4-enable-multi-factor-authentication"></a>[Opcjonalnie] Część 4: Włączanie uwierzytelniania wieloskładnikowego
Zdecydowanie zalecane jest skonfigurowanie jednego hello kilka opcji uwierzytelnianie wieloskładnikowe. Jeśli chcesz toorequire uwierzytelnianie wieloskładnikowe, zobacz [wybierz rozwiązanie z zakresu zabezpieczeń uwierzytelniania wieloskładnikowego hello](../multi-factor-authentication/multi-factor-authentication-get-started.md). Zawiera opis każdego z rozwiązań i łączy toohelp skonfiguruj rozwiązanie hello wybranych przez użytkownika.

## <a name="part-5-verification"></a>Część 5: Weryfikacja
wdrożenie Hello jest teraz ukończona, a można wypróbować niektóre scenariusze. Użyj następujących hello łączy tooexperiment z usługą hello i zapoznać się z jego funkcji.

| Zadanie | Dokumentacja |
| --- | --- |
| Dołącz do miejsca pracy niektórych urządzeń tooyour przy użyciu usługi rejestracji urządzeń usługi Azure Active Directory. Możesz także dołączyć do systemu iOS, Windows i urządzeń z systemem Android. |[Dołącz do miejsca pracy tooyour urządzeń przy użyciu usługi rejestracji urządzeń usługi Azure Active Directory](#join-devices-to-your-workplace-using-azure-active-directory-device-registration) |
| Wyświetl i włączyć lub wyłączyć zarejestrowanych urządzeń za pomocą portalu administratora hello. W tym zadaniu za pomocą portalu administratora hello wyświetlić niektórych zarejestrowanych urządzeń. |[Omówienie usługi rejestracji urządzeń usługi Azure Active Directory](active-directory-device-registration-get-started.md) |
| Sprawdź, czy obiekty urządzeń są zapisywane z usługi Azure Active Directory tooWindows serwera usługi Active Directory. |[Sprawdź, czy zarejestrowanych urządzeń są zapisywane tooActive katalogu](#verify-registered-devices-are-written-back-to-active-directory) |
| Teraz, gdy użytkownicy mogą zarejestrować swoje urządzenia, aplikację można utworzyć zasady dostępu w usługach AD FS, który zezwala tylko zarejestrowane urządzenia. To zadanie służy do tworzenia reguł dostępu do aplikacji i niestandardowy komunikat odmowy dostępu. |[Tworzenie zasad dostępu do aplikacji i niestandardowego komunikatu o odmowie dostępu](#create-an-application-access-policy-and-custom-access-denied-message) |

## <a name="integrate-azure-active-directory-with-on-premises-active-directory"></a>Integrowanie usługi Azure Active Directory z lokalną usługą Active Directory
Ten krok umożliwia zintegrowanie dzierżawy usługi Azure AD z lokalnej usługi Active Directory za pomocą usługi Azure AD Connect. Chociaż kroki hello są dostępne w hello klasycznego portalu Azure, Zanotuj wszelkie specjalne instrukcje, które są wymienione w tej sekcji.

1. Zaloguj się toohello klasycznego portalu Azure przy użyciu konta, które jest administratorem globalnym w usłudze Azure AD.
2. W okienku po lewej stronie powitania wybierz **usługi Active Directory**.
3. Na powitania **katalogu** , a następnie wybierz katalog.
4. Wybierz hello **integracji katalogów** kartę.
5. W obszarze hello **wdrażania i zarządzania nimi** sekcji, wykonaj kroki od 1 do 3 toointegrate usługi Azure Active Directory z katalogiem lokalnym.
   
   1. Dodawanie domeny.
   2. Zainstaluj i uruchom usługi Azure AD Connect za pomocą instrukcji hello na [Instalacja niestandardowa programu Azure AD Connect](connect/active-directory-aadconnect-get-started-custom.md).
   3. Sprawdź i zarządzaj nimi synchronizacji katalogów. Instrukcje rejestracji jednokrotnej są dostępne w ramach tego kroku.
   
   Ponadto, konfigurowanie federacji z usługami AD FS w sposób opisany w [Instalacja niestandardowa programu Azure AD Connect](connect/active-directory-aadconnect-get-started-custom.md).

## <a name="upgrade-your-active-directory-domain-services-schema"></a>Uaktualnienia schematu do usług domenowych w usłudze Active Directory
> [!NOTE]
> Po uaktualnieniu schemat usługi Active Directory hello procesu jest nieodwracalne. Zaleca się najpierw wykonać uaktualnienie hello w środowisku testowym.
> 

1. Zaloguj się tooyour kontrolera domeny przy użyciu konta, które ma uprawnienia administratora schematu i administratora przedsiębiorstwa.
2. Hello kopiowania **\support\adprep [media]** tooone katalogu i jego podkatalogach kontrolerów domeny usługi Active Directory (gdzie **[media]** jest nośnik instalacyjny systemu Windows Server 2012 R2 hello ścieżka toohello ).
4. W wierszu polecenia przejdź toohello **adprep** katalogu i uruchom **adprep.exe/forestprep**. Wykonaj uaktualnienie schematu hello toocomplete instrukcjami wyświetlanymi na ekranie powitania.

## <a name="prepare-your-active-directory-toosupport-devices"></a>Przygotowywanie urządzenia toosupport usługi Active Directory
> [!NOTE]
> Jest to jednorazowa operacja, że należy uruchomić tooprepare urządzenia toosupport lasu usługi Active Directory. toocomplete tę procedurę, użytkownik musi zalogować się przy użyciu uprawnień administratora przedsiębiorstwa i lasu usługi Active Directory musi mieć hello schematu systemu Windows Server 2012 R2.
> 


### <a name="prepare-your-active-directory-forest"></a>Przygotowanie lasu usługi Active Directory
1. Na serwerze federacyjnym Otwórz okno poleceń programu Windows PowerShell, a następnie wpisz **ADDeviceRegistration zainicjować**. 
2. Po wyświetleniu monitu o **ServiceAccountName**, wprowadź nazwę hello konta usługi hello wybrany jako hello konta usługi dla usług AD FS. Jeśli konto usługi zarządzane przez grupę, wprowadź konto hello w hello **domain\accountname$** format. Dla konta domeny, użyj formatu hello **domain\accountname**.

### <a name="enable-device-authentication-in-ad-fs"></a>Włącz uwierzytelnianie urządzeń w usługach AD FS
1. Na serwerze federacyjnym, otwórz konsolę zarządzania hello usług AD FS i przejść za**usług AD FS** > **zasady uwierzytelniania**.
2. Na powitania **akcje** okienku wybierz **Edytuj globalne uwierzytelnianie podstawowe**.
3. Sprawdź **Włącz uwierzytelnianie urządzeń**, a następnie wybierz **OK**.
4. Domyślnie usługi AD FS okresowo usuwa nieużywane urządzenia z usługi Active Directory. To zadanie należy wyłączyć, gdy używasz usługi rejestracji urządzeń usługi Azure Active Directory, dzięki czemu będzie można zarządzać urządzeniami w systemie Azure.

### <a name="disable-unused-device-cleanup"></a>Wyłącz oczyszczania nieużywanych urządzeń
Na serwerze federacyjnym Otwórz okno poleceń programu Windows PowerShell, a następnie wpisz **Set AdfsDeviceRegistration - MaximumInactiveDays 0**.

### <a name="prepare-azure-ad-connect-for-device-writeback"></a>Przygotowanie Azure AD Connect dla zapisu zwrotnego urządzeń
Wypełnia część 1: przygotowanie Azure AD Connect.

## <a name="join-devices-tooyour-workplace-by-using-azure-active-directory-device-registration-service"></a>Dołącz do miejsca pracy tooyour urządzeń przy użyciu usługi rejestracji urządzeń usługi Azure Active Directory

### <a name="join-an-ios-device-by-using-azure-active-directory-device-registration"></a>Dołączanie urządzenia z systemem iOS przy użyciu rejestracji urządzeń usługi Azure Active Directory
Rejestracja urządzenia w usłudze Azure Active Directory używa procesu rejestracji hello profilu bezprzewodowego dla urządzeń z systemem iOS. Ten proces uruchamia się, gdy użytkownik hello łączy toohello profilu rejestracji URL z przeglądarki Safari. format adresu URL Hello jest następujący:

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/"yourdomainname"

W takim przypadku `yourdomainname` jest nazwą domeny hello skonfigurowanego w usłudze Azure Active Directory. Na przykład jeśli nazwa domeny to contoso.com, adres URL hello wygląda następująco:

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/contoso.com

Istnieje wiele różnych sposobów toocommunicate to użytkownicy tooyour adresu URL. Na przykład jedną metodę, zalecane jest publikowanie tego adresu URL w aplikacji niestandardowej komunikatu o odmowie dostępu w usługach AD FS. Informacje te są objęte w następnej sekcji hello [Tworzenie zasad dostępu do aplikacji i niestandardowego komunikatu o odmowie dostępu](#create-an-application-access-policy-and-custom-access-denied-message).

### <a name="join-a-windows-81-device-by-using-azure-active-directory-device-registration"></a>Dołączanie urządzenia Windows 8.1 przy użyciu rejestracji urządzeń usługi Azure Active Directory
1. Na urządzeniu Windows 8.1, wybierz **ustawienia komputera** > **sieci** > **pracy**.
2. Wprowadź nazwę użytkownika w formacie nazwy UPN. na przykład  **dan@contoso.com** .
3. Wybierz **Join**.
4. Po wyświetleniu monitu zaloguj się przy użyciu poświadczeń. Witaj urządzenie zostało przyłączone.

### <a name="join-a-windows-7-device-by-using-azure-active-directory-device-registration"></a>Dołączanie urządzenia z systemem Windows 7 przy użyciu rejestracji urządzeń usługi Azure Active Directory
urządzenia przyłączone do domeny systemu Windows 7 tooregister należy pakiet oprogramowania rejestracji urządzenia hello toodeploy. Hello pakiet oprogramowania jest nazywany pracy Dołącz dla systemu Windows 7, a dostępne do pobrania na powitania [witryny sieci Web Microsoft Connect](https://connect.microsoft.com/site1164). 

Instrukcje dotyczące sposobu toouse hello pakietu są dostępne w [jak tooconfigure automatycznej rejestracji systemu Windows przyłączone do domeny urządzenia w usłudze Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).

## <a name="verify-that-registered-devices-are-written-back-tooactive-directory"></a>Sprawdź, czy zarejestrowanych urządzeń są zapisywane tooActive katalogu
Możesz wyświetlić i sprawdź, czy obiekty urządzenia został napisany ponownie tooyour usługi Active Directory przy użyciu LDP.exe lub ADSI Edit. Oba są dostępne narzędzia administratora usługi Active Directory hello.

Domyślnie obiekty urządzeń są zapisywane z usługi Azure Active Directory są umieszczane w hello sam domeny jako farmę usług AD FS.

    CN=RegisteredDevices,defaultNamingContext

## <a name="create-an-application-access-policy-and-custom-access-denied-message"></a>Tworzenie zasad dostępu do aplikacji i niestandardowego komunikatu o odmowie dostępu
Należy wziąć pod uwagę powitania po scenariusz: tworzenie aplikacji zaufania jednostki uzależnionej w usługach AD FS i skonfigurować regułę autoryzacji wystawiania, który umożliwia tylko zarejestrowane urządzenia. Tylko urządzenia, które są zarejestrowane mogą teraz tooaccess hello aplikacji. 

toomake ułatwiają aplikacji toohello toogain dostępu użytkowników, skonfigurować niestandardowy komunikat odmowy dostępu, który zawiera instrukcje toojoin swoich urządzeń. Teraz użytkownicy mają tooregister swobodne swoich urządzeń, można uzyskać dostępu do aplikacji.

Witaj poniższej procedurze pokazano, jak tooimplement tego scenariusza.

> [!NOTE]
> W tej sekcji założono, że została już skonfigurowana zaufania jednostki uzależnionej dla aplikacji w usługach AD FS.
> 

1. Otwórz hello narzędzie AD FS MMC, a następnie wybierz **usług AD FS** > **relacje zaufania** > **zaufania jednostek uzależnionych**.
2. Zlokalizuj toowhich aplikacji hello, których dotyczy ta nowa reguła dostępu. Kliknij prawym przyciskiem myszy aplikacji hello, a następnie wybierz **Edycja reguł oświadczeń**.
3. Wybierz hello **reguł autoryzacji wystawiania** , a następnie wybierz **Dodaj regułę**.
4. Z hello **reguły oświadczeń** szablonu listy rozwijanej wybierz pozycję **akceptowanie lub odrzucanie użytkowników na podstawie oświadczenia przychodzącego**. Następnie wybierz **dalej**.
5. W hello **nazwy reguły oświadczeń** wpisz **zezwolenie na dostęp z urządzeń zarejestrowanych**.
6. Z hello **typ oświadczenia przychodzącego** listy rozwijanej wybierz **użytkownik jest zarejestrowany**.
7. W hello **wartość oświadczenia przychodzącego** wpisz **true**.
8. Wybierz hello **toousers dostępu zezwolenia na podstawie tego oświadczenia przychodzącego** przycisk radiowy.
9. Wybierz **Zakończ**, a następnie wybierz **Zastosuj**.
10. Usuń wszystkie reguły, które są mniej ograniczająca niż reguły hello, utworzony. Na przykład usunąć reguły domyślnej hello **tooall zezwolenie na dostęp użytkowników**.

Aplikacja jest teraz skonfigurowany tooallow dostęp tylko wtedy, gdy użytkownik hello pochodzi z urządzenia zarejestrowane i przyłączone do miejsca pracy toohello. Aby dostęp do bardziej zaawansowanych zasad, zobacz [zarządzanie ryzykiem przy użyciu dodatkowego uwierzytelniania wieloskładnikowego dla aplikacji zawierających poufne dane](https://technet.microsoft.com/library/dn280949.aspx).

Następnie należy skonfigurować niestandardowy komunikat o błędzie dla aplikacji. komunikat o błędzie Hello umożliwia użytkownikom wiedzieć, że ich musi zostać dołączony do ich pracy toohello urządzenia przed uzyskaniem dostępu do aplikacji hello. Przy użyciu niestandardowego kodu HTML i programu PowerShell, można utworzyć niestandardową aplikację komunikat odmowy dostępu.

Na serwerze federacyjnym Otwórz okno poleceń programu PowerShell, a następnie wpisz następujące polecenie hello. Zastąp części polecenia hello elementów, które są określone tooyour systemu:

    Set-AdfsRelyingPartyWebContent -Name "relying party trust name" -ErrorPageAuthorizationErrorMessage
Należy zarejestrować urządzenie, aby korzystać z tej aplikacji.

**Jeśli używasz urządzenia z systemem iOS, wybierz ten link toojoin urządzenia**:

    a href='https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/yourdomain.com

Dołącz do tego miejsca pracy tooyour urządzenia z systemem iOS.

Jeśli używasz urządzenia Windows 8.1, można dołączyć urządzenie, wybierając **ustawienia komputera**> **sieci** > **pracy**.

W hello poprzedzających poleceń **jednostki uzależnionej Nazwa zaufania jednostki** jest nazwą hello obiektu zaufania jednostki uzależnionej aplikacji w usługach AD FS.
I **twoja_domena.com** jest hello nazwy domeny, które zostały skonfigurowane w usłudze Azure Active Directory (na przykład contoso.com).
Można tooremove się, że wszystkie podziały wierszy (jeśli istnieją) z hello HTML zawartości, że przekazujesz toohello **AdfsRelyingPartyWebContent zestaw** polecenia cmdlet.

Teraz, gdy użytkownicy uzyskują dostęp do aplikacji z urządzenia, które nie jest zarejestrowany w hello usługi rejestracji urządzeń usługi Azure Active Directory, zostanie wyświetlona strona, która wygląda podobnie toohello następującego zrzutu ekranu.

![Zrzut ekranu przedstawiający wystąpił błąd, gdy użytkownicy nie został zarejestrowany na urządzeniu z usługą Azure AD](./media/active-directory-conditional-access/error-azureDRS-device-not-registered.gif)


