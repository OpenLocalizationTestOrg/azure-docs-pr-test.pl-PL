---
title: "aaaMFA serwera z usługami AD FS w systemie Windows Server | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooget do korzystania z usługi Azure Multi-Factor Authentication i usług AD FS w systemie Windows Server 2012 R2 i 2016."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 57208068-1e55-45b6-840f-fdcd13723074
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/29/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 656785abcc63a020add765a86670b488a3b84b51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-in-windows-server"></a>Konfigurowanie serwera usługi Azure Multi-Factor Authentication toowork z usługami AD FS w systemie Windows Server
Jeśli korzystasz z usługi Active Directory Federation Services (AD FS) i mają toosecure zasobów chmury lub lokalnymi, można skonfigurować serwera usługi Azure Multi-Factor Authentication toowork z usługami AD FS. Ta konfiguracja wyzwala weryfikację dwuetapową dla punktów końcowych o wysokiej wartości.

W tym artykule omawiane jest korzystanie z serwera usługi Azure Multi-Factor Authentication oraz usług AD FS w systemie Windows Server 2012 R2 lub Windows Server 2016. Aby uzyskać więcej informacji, przeczytaj temat zbyt[zabezpieczanie zasobów w chmurze i lokalnych przy użyciu serwera usługi Azure Multi-Factor Authentication z usługami AD FS 2.0](multi-factor-authentication-get-started-adfs-adfs2.md).

## <a name="secure-windows-server-ad-fs-with-azure-multi-factor-authentication-server"></a>Zabezpieczanie usług AD FS systemu Windows Server za pomocą serwera usługi Azure Multi-Factor Authentication
Po zainstalowaniu serwera usługi Azure Multi-Factor Authentication, masz hello następujące opcje:

* Instalowanie serwera usługi Azure Multi-Factor Authentication lokalnie na powitania tym samym serwerze co usługi AD FS
* Zainstaluj hello Azure Multi-Factor Authentication karty lokalnie na powitania serwera usług AD FS, a następnie zainstaluj aplikację serwer Multi-Factor Authentication na innym komputerze

Przed rozpoczęciem należy pamiętać o hello następujących informacji:

* Nie masz wymaganych tooinstall serwera usługi Azure Multi-Factor Authentication na serwerze usług AD FS. Jednak należy zainstalować hello karty uwierzytelniania wieloskładnikowego usług AD FS w systemie Windows Server 2012 R2 lub Windows Server 2016 z systemem usług AD FS. Powitania serwera można zainstalować na innym komputerze, jeśli jest obsługiwana wersja i oddzielnie zainstalować hello adapter AD FS na serwerze federacyjnym usług AD FS. Zobacz hello następujących procedur toolearn jak tooinstall hello karty oddzielnie.
* Jeśli organizacja korzysta z wiadomości SMS lub metody weryfikacji w aplikacji mobilnej, hello ciągi zdefiniowane w sekcji Ustawienia firmy zawiera symbol zastępczy <$*nazwa_aplikacji*$>. Na serwerze usługi MFA w wersji 7.1 możesz podać nazwę aplikacji, która zastępuje ten symbol zastępczy. W v7.0 lub starszych ten symbol zastępczy nie jest automatycznie zastępowany używania hello AD FS karty. Dla tych starszych wersji należy usunąć symbol zastępczy hello z hello odpowiednie ciągi zabezpieczenie usług AD FS.
* Witaj konta toosign w musi mieć grup zabezpieczeń toocreate praw użytkownika w usłudze Active Directory.
* Kreator instalacji karty Hello uwierzytelnianie wieloskładnikowe AD FS tworzy grupę zabezpieczeń o nazwie PhoneFactor Admins w wystąpieniu usługi Active Directory. Dodaje konto usługi hello usług AD FS grupy toothis usługi federacyjnej. Sprawdź na kontrolerze domeny, że powitalne rzeczywiście została utworzona grupa PhoneFactor Admins i że konto usługi hello AD FS jest członkiem tej grupy. Jeśli to konieczne, należy ręcznie dodać hello usług AD FS usługi konta toohello grupy PhoneFactor Admins na kontrolerze domeny.
* Informacje o instalowaniu hello zestawu SDK usług sieci Web za pomocą portalu użytkownika hello, przeczytaj o [wdrażanie hello portal użytkowników dla serwera usługi Azure Multi-Factor Authentication.](multi-factor-authentication-get-started-portal.md)

### <a name="install-azure-multi-factor-authentication-server-locally-on-hello-ad-fs-server"></a>Instalowanie serwera usługi Azure Multi-Factor Authentication lokalnie na serwerze hello usług AD FS
1. Pobierz serwer Azure Multi-Factor Authentication i zainstaluj go na serwerze usług AD FS. Aby uzyskać informacje dotyczące instalacji, przeczytaj o [wprowadzeniu do serwera Azure Multi-Factor Authentication](multi-factor-authentication-get-started-server.md).
2. W konsoli zarządzania serwera usługi Azure Multi-Factor Authentication powitania kliknij hello **usług AD FS** ikony. Wybierz opcje hello **Zezwalaj na rejestrację użytkowników** i **użytkownicy metody tooselect**.
3. Wybierz dodatkowe opcje chcesz toospecify dla Twojej organizacji.
4. Kliknij pozycję **Zainstaluj adapter ADFS**.
   
   <center>![Chmura](./media/multi-factor-authentication-get-started-adfs-w2k12/server.png)</center>

5. Jeśli zostanie wyświetlone okno usługi Active Directory hello, oznacza to dwie czynności. Ten komputer jest tooa przyłączone do domeny, a hello konfiguracji usługi Active Directory do zabezpieczenia komunikacji między hello AD FS karty a usługą Multi-Factor Authentication hello jest niekompletna. Kliknij przycisk **dalej** tooautomatically wprowadzić tę konfigurację, lub wybierz hello **Pomiń automatyczną konfigurację usługi Active Directory i wprowadź ustawienia ręcznie** pole wyboru. Kliknij przycisk **Dalej**.
6. Jeśli windows grupy lokalne powitania jest wyświetlana, oznacza to dwie czynności. Twój komputer nie jest tooa przyłączone do domeny, a konfiguracja grupy lokalnej hello do zabezpieczania komunikacji między adapterem FS hello AD a hello usługi Multi-Factor Authentication jest ukończona. Kliknij przycisk **dalej** tooautomatically wprowadzić tę konfigurację, lub wybierz hello **Pomiń automatyczną konfigurację grupy lokalnej i wprowadź ustawienia ręcznie** pole wyboru. Kliknij przycisk **Dalej**.
7. W Kreatorze instalacji powitania kliknij **dalej**. Azure aplikacji serwer Multi-Factor Authentication tworzy hello grupy PhoneFactor Admins i dodaje hello usług AD FS usługi konta toohello grupy PhoneFactor Admins.
   <center>![Chmura](./media/multi-factor-authentication-get-started-adfs-w2k12/adapter.png)</center>
8. Na powitania **uruchomienie Instalatora** kliknij przycisk **dalej**.
9. W Instalatorze karty hello uwierzytelnianie wieloskładnikowe AD FS, kliknij przycisk **dalej**.
10. Kliknij przycisk **Zamknij** po zakończeniu instalacji hello.
11. Po zainstalowaniu hello karty musi być zarejestrowany za pomocą usług AD FS. Otwórz program Windows PowerShell i uruchom następujące polecenie hello:<br>
    `C:\Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1`
    <center>![Chmura](./media/multi-factor-authentication-get-started-adfs-w2k12/pshell.png)</center>
12. toouse Twojego adaptera nowo zarejestrowanych edycji hello globalne zasady uwierzytelniania w usługach AD FS. W konsoli zarządzania hello AD FS Przejdź toohello **zasady uwierzytelniania** węzła. W hello **uwierzytelnianie wieloskładnikowe** kliknij hello **Edytuj** link dalej toohello **ustawienia globalne** sekcji. W hello **Edytuj globalne zasady uwierzytelniania** wybierz **uwierzytelnianie wieloskładnikowe** jako dodatkową metodę uwierzytelniania, a następnie kliknij przycisk **OK**. Witaj adapter jest rejestrowany jako element WindowsAzureMultiFactorAuthentication. Uruchom ponownie usługę hello AD FS hello rejestracji tootake efekt.

<center>![Chmura](./media/multi-factor-authentication-get-started-adfs-w2k12/global.png)</center>

W tym momencie serwer Multi-Factor Authentication jest skonfigurowany toobe toouse dostawcy dodatkowego uwierzytelniania przy użyciu usług AD FS.

## <a name="install-a-standalone-instance-of-hello-ad-fs-adapter-by-using-hello-web-service-sdk"></a>Instalowanie wystąpienia autonomicznego karty hello usług AD FS przy użyciu hello zestawu SDK usług sieci Web
1. Zainstaluj hello zestawu SDK usług sieci Web na powitania serwera, który jest uruchomiony serwer Multi-Factor Authentication.
2. Następujące hello kopiowania plików z hello \Program Files\Multi-toohello serwer katalogowy serwer Multi-Factor Authentication, na którym planujesz tooinstall hello AD FS karty:
   * MultiFactorAuthenticationAdfsAdapterSetup64.msi
   * Register-MultiFactorAuthenticationAdfsAdapter.ps1
   * Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
   * MultiFactorAuthenticationAdfsAdapter.config
3. Uruchom plik instalacyjny MultiFactorAuthenticationAdfsAdapterSetup64.msi hello.
4. W Instalatorze karty hello uwierzytelnianie wieloskładnikowe AD FS, kliknij przycisk **dalej** toostart hello instalacji.
5. Kliknij przycisk **Zamknij** po zakończeniu instalacji hello.

## <a name="edit-hello-multifactorauthenticationadfsadapterconfig-file"></a>Przeprowadź edycję pliku MultiFactorAuthenticationAdfsAdapter.config hello
Wykonaj te kroki tooedit hello MultiFactorAuthenticationAdfsAdapter.config pliku:

1. Zestaw hello **UseWebServiceSdk** węzła zbyt**true**.  
2. Ustaw wartość hello **dla węzła WebServiceSdkUrl** toohello adres URL hello usługi Multi-Factor Authentication Web Service SDK. Na przykład: *https://contoso.com/&lt;certificatename&gt;/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx*, gdzie *certificatename* jest hello nazwę certyfikatu.  
3. Edytowanie skryptu hello Register-MultiFactorAuthenticationAdfsAdapter.ps1 przez dodanie *- ConfigurationFilePath &lt;ścieżki&gt;*  toohello koniec hello `Register-AdfsAuthenticationProvider` polecenie, gdzie  *&lt;ścieżki&gt;*  jest pliku MultiFactorAuthenticationAdfsAdapter.config toohello pełną ścieżkę hello.

### <a name="configure-hello-web-service-sdk-with-a-username-and-password"></a>Konfigurowanie hello zestawu SDK usług sieci Web przy użyciu nazwy użytkownika i hasła
Dostępne są dwie opcje dotyczące konfigurowania hello zestawu SDK usług sieci Web. Witaj najpierw przy użyciu nazwy użytkownika i hasła, hello drugi jest przy użyciu certyfikatu klienta. Wykonaj następujące kroki dla pierwszej opcji hello lub przejść od razu do hello drugi.  

1. Ustaw wartość hello **WebServiceSdkUsername** tooan konta, które jest członkiem grupy zabezpieczeń PhoneFactor Admins hello. Użyj hello &lt;domeny&gt;&#92;&lt; Nazwa użytkownika&gt; format.  
2. Ustaw wartość hello **dla węzła WebServiceSdkPassword** toohello odpowiednie hasło konta.

### <a name="configure-hello-web-service-sdk-with-a-client-certificate"></a>Konfigurowanie hello zestawu SDK usług sieci Web z certyfikatem klienta
Jeśli nie chcesz toouse nazwy użytkownika i hasła, wykonaj te kroki tooconfigure hello zestawu SDK usług sieci Web z certyfikatem klienta.

1. Uzyskaj certyfikat klienta z urzędu certyfikacji w celu hello serwer z systemem hello zestawu SDK usług sieci Web. Dowiedz się, jak za[uzyskiwanie certyfikatów klienta](https://technet.microsoft.com/library/cc770328.aspx).  
2. Importu powitania klienta certyfikatu toohello lokalnym magazynie certyfikatów osobistych komputera na powitania serwera, który działa hello zestawu SDK usług sieci Web. Upewnij się, że certyfikat publiczny tego urzędu certyfikacji hello znajduje się w magazynie certyfikatów zaufanych certyfikatów głównych.  
3. Wyeksportuj klucze publiczne i prywatne hello hello — pliku PFX tooa certyfikatu klienta.  
4. Wyeksportuj klucz publiczny hello w pliku .cer tooa formatu Base64.  
5. W Menedżerze serwera sprawdź, czy jest zainstalowana funkcja Uwierzytelnianie mapowań certyfikatów klientów \Web Server\Security\IIS ta hello serwer sieci Web (IIS). Jeśli nie jest zainstalowany, wybierz **Dodaj role i funkcje** tooadd tej funkcji.  
6. W Menedżerze usług IIS kliknij dwukrotnie **edytora konfiguracji** w hello witryny sieci Web, która zawiera katalog wirtualny zestawu SDK usług sieci Web hello. Jest ważne tooselect hello witryny sieci Web, nie hello katalogu wirtualnego.  
7. Przejdź toohello **system.webServer/security/authentication/iisClientCertificateMappingAuthentication** sekcji.  
8. Zestaw włączane za**true**.  
9. Ustaw dla węzła oneToOneCertificateMappingsEnabled zbyt**true**.  
10. Kliknij przycisk hello **...**  przycisku Dalej toooneToOneMappings, a następnie kliknij przycisk hello **Dodaj** łącza.  
11. Otwórz plik cer Base64 hello wyeksportowany wcześniej. Usuń wiersze *-----BEGIN CERTIFICATE-----* i *-----END CERTIFICATE-----* oraz wszystkie podziały wierszy. Skopiuj wynikowy ciąg hello.  
12. Zestaw certyfikatu toohello ciąg skopiowany w hello poprzedzających krok.  
13. Zestaw włączane za**true**.  
14. Ustaw konto tooan nazwy użytkownika, które jest członkiem grupy zabezpieczeń PhoneFactor Admins hello. Użyj hello &lt;domeny&gt;&#92;&lt; Nazwa użytkownika&gt; format.  
15. Ustaw hello hasła toohello odpowiednie hasło konta, a następnie zamknij Edytor konfiguracji.  
16. Kliknij przycisk hello **Zastosuj** łącza.  
17. W katalogu wirtualnego zestawu SDK usług sieci Web hello, kliknij dwukrotnie **uwierzytelniania**.  
18. Sprawdź, czy personifikacja ASP.NET i uwierzytelnianie podstawowe są zbyt**włączone**, oraz czy wszystkie inne elementy są ustawiane za**wyłączone**.  
19. W katalogu wirtualnego zestawu SDK usług sieci Web hello, kliknij dwukrotnie **ustawienia protokołu SSL**.  
20. Ustaw certyfikaty klienta zbyt**Zaakceptuj**, a następnie kliknij przycisk **Zastosuj**.  
21. Skopiuj plik PFX hello wyeksportowany wcześniej serwera toohello uruchomionym hello adapter AD FS.  
22. Importuj magazynu certyfikatów osobistych komputera lokalnego pliku toohello hello pfx.  
23. Kliknij prawym przyciskiem myszy i wybierz **Zarządzaj kluczami prywatnymi**, a następnie Udziel dostępu do odczytu toohello konto używane toosign toohello AD FS usługi.  
24. Otwórz powitania klienta certyfikatu i skopiuj hello odcisk palca z hello **szczegóły** kartę.  
25. W pliku MultiFactorAuthenticationAdfsAdapter.config hello ustaw **dla węzła WebServiceSdkCertificateThumbprint** toohello ciąg skopiowany w poprzednim kroku hello.  

Na koniec tooregister hello karty, uruchom hello \Program Files\Multi-Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1 skryptu w programie PowerShell. Witaj adapter jest rejestrowany jako element WindowsAzureMultiFactorAuthentication. Uruchom ponownie usługę hello AD FS hello rejestracji tootake efekt.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>Zabezpieczanie zasobów usługi Azure AD za pomocą usług AD FS
toosecure zasób chmury, ustaw reguły oświadczeń Active Directory Federation Services emituje hello multipleauthn oświadczenia, gdy użytkownik wykona pomyślnie weryfikacji dwuetapowej. Tego oświadczenia są przekazywane tooAzure AD. Wykonaj tej procedury toowalk hello kroki:

1. Otwórz przystawkę zarządzania usługami AD FS.
2. Po lewej stronie powitania, wybierz **zaufania jednostek uzależnionych**.
3. Kliknij prawym przyciskiem myszy pozycję **Platforma tożsamości usługi Microsoft Office 365** i wybierz pozycję **Edytuj reguły oświadczeń...**

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. Na karcie Reguły przekształcania wystawiania kliknij pozycję **Dodaj regułę**.

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. Na hello przekształcenie Kreatorze dodawania reguły oświadczenia, wybierz **przekazuj lub Filtruj oświadczenie przychodzące** z hello listy rozwijanej, a następnie kliknij przycisk **dalej**.

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Nadaj regule nazwę.
7. Wybierz **odwołania do metod uwierzytelniania** hello przychodzące typ oświadczenia.
8. Wybierz pozycję **Przekazuj wszystkie wartości oświadczeń**.
    ![Kreator dodawania reguły przekształcania dotyczącej oświadczeń](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. Kliknij przycisk **Zakończ**. Zamknij konsolę zarządzania FS hello AD.

## <a name="related-topics"></a>Powiązane tematy
Aby uzyskać pomoc dotycząca rozwiązywania problemów, zobacz hello [Azure Multi-Factor Authentication — często zadawane pytania](multi-factor-authentication-faq.md)
