---
title: "aaaAzure uwierzytelnianie wieloskładnikowe — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania i odpowiedzi dotyczące tooAzure usługi Multi-Factor Authentication. Uwierzytelnianie wieloskładnikowe jest metodą weryfikacji tożsamości użytkownika, który wymaga więcej niż nazwy użytkownika i hasła. Zapewnia dodatkową warstwę zabezpieczeń toouser logowania i transakcji."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8305cf4c41bf8e9802df192fecdb7e463eff9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-multi-factor-authentication"></a>Często zadawane pytania dotyczące usługi Azure Multi-Factor Authentication
Często zadawane pytania dotyczące usługi Azure Multi-Factor Authentication i przy użyciu usługi Multi-Factor Authentication hello odpowiedzi na często zadawane pytania. Go dzieli się na pytania dotyczące usługi hello ogólnie rzecz biorąc, rozliczeń modeli, możliwości użytkowników i rozwiązywania problemów.

## <a name="general"></a>Ogólne
**Pytanie: jak serwera usługi Azure Multi-Factor Authentication obsługuje dane użytkownika?**

Serwer Multi-Factor Authentication tylko na serwerach lokalnych hello są przechowywane dane użytkownika. Brak danych trwałych użytkownika są przechowywane w chmurze hello. Gdy użytkownik hello przeprowadza weryfikację dwuetapową, serwer Multi-Factor Authentication wysyła toohello danych usługi w chmurze Azure Multi-Factor Authentication do uwierzytelniania. Komunikacja między aplikacji serwer Multi-Factor Authentication i hello usługi w chmurze usługi Multi-Factor Authentication używa protokołu Secure Sockets Layer (SSL) lub zabezpieczeń TLS (Transport Layer) za pośrednictwem portu 443 dla ruchu wychodzącego.

Podczas żądania uwierzytelnienia wysyłane toohello usługi w chmurze, dane są zbierane dla uwierzytelniania i użycia raporty. Pola danych zawarte w dziennikach weryfikacji dwuetapowej są następujące:

* **Unikatowy identyfikator** (albo nazwę lub lokalnymi usługi Multi-Factor Authentication serwera identyfikator użytkownika)
* **Pierwszy i nazwisko** (opcjonalnie)
* **Adres e-mail** (opcjonalnie)
* **Numer telefonu** (w przypadku używania połączenie głosowe lub uwierzytelniania programu SMS)
* **Token urządzenia** (w przypadku używania uwierzytelniania aplikacji mobilnej)
* **Tryb uwierzytelniania**
* **Wynik uwierzytelniania**
* **Nazwa serwera usługi Multi-Factor Authentication**
* **Serwer usługi Multi-Factor Authentication IP**
* **Klient IP** (jeśli jest dostępny)

można skonfigurować Hello pola opcjonalne w aplikacji serwer Multi-Factor Authentication.

Witaj wynik weryfikacji (powodzenie lub odmowę) i hello Przyczyna jeśli odmówiono, znajduje się z danymi uwierzytelniania hello. Te dane są dostępne w sekcji uwierzytelnianie i raportów użycia.

## <a name="billing"></a>Rozliczenia
Większość pytań związanych z rozliczeniami można odpowiedzi, odnosząc się tooeither hello [stronie cennika usługi Multi-Factor Authentication](https://azure.microsoft.com/pricing/details/multi-factor-authentication/) lub hello dokumentację dotyczącą [jak tooget Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md).

**Pyt.: czy Moja organizacja naliczona opłata za wysyłanie hello połączenia telefoniczne i wiadomości tekstowych, które są używane do uwierzytelniania?**

Nie, nie są naliczane opłaty dla poszczególnych połączeń telefonicznych umieszczone lub tekst wiadomości wysyłane toousers za pośrednictwem usługi Azure Multi-Factor Authentication. Jeśli używasz dostawcy usługi MFA dla uwierzytelniania są rozliczane podczas każdego uwierzytelniania, ale nie dla hello metodę.

Użytkownicy mogą naliczona opłata za połączenia telefoniczne hello lub tekst wiadomości, które otrzymają, zgodnie z tootheir Telefon osobisty usługi.

**Pytanie: czy modelu rozliczeń na użytkownika hello naliczają opłaty dla wszystkich aktywnych użytkowników lub hello tylko te, które są wykonywane weryfikację dwuetapową?**

Rozliczenia jest oparta na powitania liczba toouse użytkownicy, uwierzytelnianie wieloskładnikowe, niezależnie od tego, czy one przeprowadzone weryfikacji dwuetapowej miesiąca.

**Pytanie: jak działa rozliczanie uwierzytelnianie wieloskładnikowe?**

Podczas tworzenia dostawcy usługi MFA dla poszczególnych użytkowników lub uwierzytelnienia w organizacji subskrypcji platformy Azure jest rozliczane co miesiąc na podstawie użycia. Przypomina to modelu rozliczeń toohow Azure rachunków użycia maszyn wirtualnych i witryn sieci Web.

Po zakupie subskrypcji dla usługi Azure Multi-Factor Authentication organizacji tylko płaci hello opłata licencji dla każdego użytkownika. Licencje MFA i usługi Office 365, Azure AD Premium lub pakietu Enterprise Mobility + pakietów zabezpieczeń są rozliczane w ten sposób. 

Dowiedz się więcej na temat opcji znajduje się w [jak tooget Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md).

**Pytanie: istnieje już bezpłatna wersja Azure Multi-Factor Authentication?**

W niektórych przypadkach tak.

Uwierzytelnianie wieloskładnikowe dla administratorów usługi Azure oferuje podzbiór funkcji usługi Azure MFA bez ponoszenia kosztów dostępu tooMicrosoft usług online, w tym hello portali administratora platformy Azure i usługi Office 365. Ta oferta dotyczy tylko administratorzy tooglobal w ramach wystąpienia usługi Azure Active Directory, które nie mają hello pełną wersję usługi Azure MFA za pośrednictwem licencji usługi MFA, pakietu lub dostawcę autonomiczny zużycia. Jeśli administratorów hello bezpłatną wersję, a następnie Kup pełną wersję usługi Azure MFA, w przypadku wszystkich administratorów globalnych są toohello z podwyższonym poziomem uprawnień, automatycznie płatnej wersji.

Uwierzytelnianie wieloskładnikowe dla użytkowników usługi Office 365 oferuje podzbiór funkcji usługi Azure MFA bez ponoszenia kosztów dla dostępu usługi 365 tooOffice, w tym usługi Exchange Online i SharePoint Online. Ta oferta dotyczy toousers, kto ma licencji usługi Office 365 przypisany, gdy hello odpowiednie wystąpienia usługi Azure Active Directory nie hello pełną wersję usługi Azure MFA za pośrednictwem licencji usługi MFA, pakietu lub dostawcę autonomiczny zużycia.

**Pytanie: czy Moja organizacja przełączać się między na użytkownika na uwierzytelnianie zużycie rozliczeń modele i w dowolnym momencie?**

Jeśli Twoja organizacja zakupi MFA jako usługi autonomicznej z rozliczania opartego na zużycie, wybierz modelu rozliczeń podczas tworzenia dostawcy usługi MFA. Nie można zmienić modelu rozliczeń hello, po utworzeniu dostawca usługi MFA. Jednak można usunąć dostawcy usługi MFA hello, a następnie utworzyć jeden z innego modelu rozliczeń.

Podczas tworzenia dostawcy usługi MFA można tooan połączonej usługi Azure Active Directory (alias "dzierżawy usługi Azure AD"). W przypadku hello bieżącego dostawcy usługi MFA dzierżawy tooan połączonej usługi Azure AD, można bezpiecznie usunąć dostawcę usługi MFA hello i utworzyć jest toohello połączonej usługi Azure AD w tej samej dzierżawy. Alternatywnie Jeśli zakupione za mało MFA, Azure AD Premium lub Enterprise Mobility + Security (EMS) licencji toocover wszystkich użytkowników, którzy są włączone dla usługi MFA, można usunąć dostawca usługi MFA hello całkowicie.

W przypadku dostawcy usługi MFA *nie* dzierżawy tooan połączonej usługi Azure AD, lub połączyć hello nowej usługi MFA dostawcy tooa różne usługi Azure AD dzierżawy, opcje konfiguracji i ustawień użytkownika nie są przenoszone. Ponadto istniejących serwerów usługi Azure MFA muszą toobe ponownie aktywować przy użyciu poświadczeń aktywacji wygenerowane za pośrednictwem hello nowy dostawca usługi MFA. Ponowne uaktywnianie hello serwerów MFA toolink ich toohello nowy dostawca usługi MFA bez wpływu połączeń telefonicznych i uwierzytelniania wiadomości tekstowych, ale aplikacji mobilnej powiadomienia przestanie działać dla wszystkich użytkowników, do czasu ich ponowne uaktywnianie hello aplikacji mobilnej.

Dowiedz się więcej o dostawców usługi MFA w [wprowadzenie do korzystania z dostawcy uwierzytelniania wieloskładnikowego Azure](multi-factor-authentication-get-started-auth-provider.md).

**Pytanie: czy Moja organizacja przełączać się między rozliczeń i subskrypcji (na podstawie licencji modelu) na podstawie zużycia w dowolnym momencie?**

W niektórych przypadkach tak.

Jeśli katalog zawiera *użytkownika* dostawcy usługi Azure Multi-Factor Authentication można dodać licencji usługi MFA. Użytkownicy mający licencje nie są zliczane w hello na użytkownika na podstawie zużycia rozliczeń. Użytkownicy nie mają licencji można nadal włączone dla usługi MFA za pośrednictwem dostawcy usługi MFA hello. Jeśli zakupu i przypisz licencje dla wszystkich użytkowników skonfigurowanych toouse uwierzytelnianie wieloskładnikowe, można usunąć dostawcy usługi Azure Multi-Factor Authentication hello. Zawsze można utworzyć innego dostawcy usługi MFA dla poszczególnych użytkowników, jeśli w przyszłości hello więcej użytkowników niż liczba licencji.

Jeśli katalog zawiera *na uwierzytelnianie* dostawcy usługi Azure Multi-Factor Authentication, są zawsze rozliczane podczas każdego uwierzytelniania tak długo, jak dostawca usługi MFA hello jest połączony tooyour subskrypcji. Można przypisać toousers licencji usługi MFA, ale nadal zostaną naliczone przy każdym żądaniu weryfikacji dwuetapowej, czy pochodzi ona z ktoś z licencją MFA lub nie.

**Pytanie: czy Moja organizacja ma toouse i zsynchronizować tożsamości toouse uwierzytelnianie wieloskładnikowe Azure?**

Jeśli Twoja organizacja korzysta z modelu rozliczeń na podstawie zużycia, Azure Active Directory jest opcjonalny, ale nie jest wymagane. Jeśli dostawcy usługi MFA nie jest połączony tooan dzierżawy usługi Azure AD, można wdrożyć tylko serwera usługi Azure Multi-Factor Authentication lub hello Azure Multi-Factor Authentication SDK lokalnie.

Usługa Azure Active Directory jest wymagana dla hello licencji modelu, ponieważ licencje są dodawane toohello dzierżawy usługi Azure AD, gdy zakupu i przypisać je toousers w katalogu hello.

## <a name="manage-and-support-user-accounts"></a>Zarządzanie i obsługę kont użytkowników

**Pytanie: co mam powiedzieć Mój toodo użytkowników jeśli ich nie otrzymują odpowiedź na telefon lub nie masz telefon z nimi?**

Miejmy nadzieję, że wszyscy użytkownicy skonfigurowany więcej niż jednej metody weryfikacji. Poinformuj ich tootry Zaloguj się ponownie, ale wybierz metodę inną weryfikacji na powitania strony logowania.

Można wskazać toohello Twojego użytkowników [przewodnik rozwiązywania problemów dla użytkowników końcowych](./end-user/multi-factor-authentication-end-user-troubleshoot.md).


**Pytanie: co należy zrobić, jeśli jeden z użytkowników nie można pobrać tootheir konta?**

Możesz przywrócić konto użytkownika hello przy nadawania toogo przez proces rejestracji hello ponownie. Dowiedz się więcej o [Zarządzanie ustawieniami użytkowników i urządzeń w usłudze Azure Multi-Factor Authentication w chmurze hello](multi-factor-authentication-manage-users-and-devices.md).

**Pytanie: co należy zrobić, jeśli jeden z użytkowników utraci telefon jest korzystanie z haseł aplikacji?**

tooprevent nieautoryzowanym dostępem, Usuń wszystkie użytkownika hello hasła aplikacji. Po hello użytkownik ma urządzenia zastępczego, można ponownie utworzyć hello hasła. Dowiedz się więcej o [Zarządzanie ustawieniami użytkowników i urządzeń w usłudze Azure Multi-Factor Authentication w chmurze hello](multi-factor-authentication-manage-users-and-devices.md).

**Pytanie: co zrobić, jeśli użytkownik nie może zalogować się w aplikacji przeglądarki toonon?**

Jeśli Twoja organizacja nadal korzysta starszych klientów, a [dozwolone stosowanie haseł aplikacji hello](multi-factor-authentication-whats-next.md#app-passwords), a następnie użytkownicy nie logują się toothese starszych klientów z swoją nazwę użytkownika i hasło. Zamiast tego muszą zbyt[skonfigurować hasła aplikacji](./end-user/multi-factor-authentication-end-user-app-passwords.md). Użytkownikom należy wyczyścić (Usuń) informacje logowania, uruchom ponownie aplikacji hello, a następnie zaloguj się przy użyciu swoją nazwę użytkownika i *hasła aplikacji* zamiast ich prawidłowe hasło.

Jeśli Twoja organizacja nie ma starszych klientów, nie należy zezwalać użytkownikom toocreate hasła aplikacji.

> [!NOTE]
> Nowoczesne uwierzytelnianie dla klientów Office 2013
>
> Hasła aplikacji są tylko niezbędne dla aplikacji, które nie obsługują nowoczesnego uwierzytelniania. Klienci Office 2013 obsługuje protokoły nowoczesnego uwierzytelniania, ale wymaga toobe skonfigurowany. Nowszych wersji klientów Office automatycznie obsługują protokoły nowoczesnego uwierzytelniania. Aby uzyskać więcej informacji, zobacz hello [anonsowania publicznej wersji zapoznawczej nowoczesnego uwierzytelniania pakietu Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).

**Pytanie: Moi użytkownicy mówią, że czasami nie otrzymują wiadomości tekstowej hello, lub ich odpowiedzi sposób tootwo wiadomości SMS, ale weryfikacji hello upłynie limit czasu.**

Dostarczenie wiadomości tekstowych i otrzymania odpowiedzi w dwukierunkowe programu SMS nie ma gwarancji, ponieważ istnieją fluktuacje czynników, które mogłyby wpłynąć na niezawodność hello hello usługi. Te czynniki obejmują hello kraju przeznaczenia, operator telefon komórkowy hello i hello siła sygnału.

Jeżeli użytkownicy często występują problemy z niezawodnie odbieranie wiadomości tekstowych, poinformuj ich toouse hello przenośnych aplikacji lub połączeń telefonicznych metody zamiast tego. Aplikacja mobilna Hello może odbierać powiadomienia zarówno za pośrednictwem połączenia sieci Wi-Fi i sieci komórkowej. Ponadto hello aplikacji mobilnej można generować kodów weryfikacyjnych nawet wtedy, gdy urządzenie hello ma wcale brak sygnału. Aplikacja Microsoft Authenticator Hello jest dostępna dla [Android](http://go.microsoft.com/fwlink/?Linkid=825072), [IOS](http://go.microsoft.com/fwlink/?Linkid=825073), i [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071).

Należy użyć wiadomości tekstowych, zaleca się przy użyciu jednokierunkowego SMS zamiast dwukierunkowe programu SMS, kiedy to możliwe. Jednokierunkowe SMS są bardziej niezawodne i uniemożliwia użytkownikom naliczania globalne opłat programu SMS z odpowiedzieć tooa wiadomość tekstowa, która została wysłana z innego kraju.

**Pytanie: czy można zmienić okres hello Moi użytkownicy mają kodu weryfikacyjnego hello tooenter z wiadomość SMS, zanim upłynie limit czasu systemu hello?**

W niektórych przypadkach tak. 

Dla jednokierunkowe SMS z serwera usługi Azure MFA v7.0 lub nowszym można skonfigurować limit czasu hello ustawienie przez ustawienie klucza rejestru. Po hello usługi MFA w chmurze wysyła wiadomość hello, kod weryfikacyjny hello (lub jednorazowy kod dostępu) jest zwracana toohello serwera usługi MFA. powitania serwera usługi MFA przechowuje kod hello w pamięci przez 300 sekund domyślnie. Jeśli użytkownik hello nie kod hello przed hello 300 sekund, odmówiono uwierzytelniania. Użyj tych kroków toochange hello domyślny limit czasu ustawienia:

1. Przejdź tooHKLM\Software\Wow6432Node\Positive Networks\PhoneFactor.
2. Utwórz klucz rejestru DWORD o nazwie **pfsvc_pendingSmsTimeoutSeconds** i ustawić hello czas w sekundach, które mają powitania serwera usługi Azure MFA toostore jednorazowe kodów dostępu.

>[!TIP] 
>Jeśli masz wiele serwerów usługi MFA, tylko hello, który hello oryginalnego żądania uwierzytelniania przetwarzane wie hello kod weryfikacyjny, który został wysłany toohello użytkownika. Gdy użytkownik hello wprowadza hello kodu, hello toovalidate żądania uwierzytelniania wymagane jest wysłanie toohello tym samym serwerze. Jeśli Weryfikacja kodu hello są wysyłane tooa inny serwer, hello uwierzytelnianie zostanie odrzucone. 

Dla dwukierunkowe SMS z serwera usługi Azure MFA można skonfigurować ustawienia limitu czasu hello w hello portalu zarządzania usługi MFA. Jeśli użytkownicy nie odpowie toohello programu SMS w hello zdefiniowanego limitu czasu, ich uwierzytelnianie zostanie odrzucone. 

Dla jednokierunkowe SMS za pomocą usługi Azure MFA w chmurze hello (w tym hello rozszerzenia serwera zasad sieciowych karty sieciowej lub hello usług AD FS) nie można skonfigurować ustawienia limitu czasu hello. Usługi Azure AD przechowuje kod weryfikacyjny hello 180 sekund. 

**Pytanie: czy można używać tokeny sprzętowe z serwera usługi Azure Multi-Factor Authentication?**

Jeśli korzystasz z serwera usługi Azure Multi-Factor Authentication, można zaimportować tokeny na podstawie czasu, jednorazowe hasła (TOTP) otwarte uwierzytelnianie (OATH) innej firmy, a następnie używać ich na potrzeby weryfikacji dwuetapowej.

Możesz użyć tokenów ActiveIdentity, które są tokenami OATH TOTP, po umieszczeniu hello klucz tajny w pliku CSV i zaimportować tooAzure aplikacji serwer Multi-Factor Authentication. Tak długo, jak powitania klienta systemu może akceptować dane wejściowe użytkownika hello, można użyć tokenów OATH z Active Directory Federation Services (ADFS), uwierzytelnianie oparte na formularzach Internet Information Server (IIS) i usługi usługi użytkowników zdalnego uwierzytelniania (RADIUS).

Tokeny OATH TOTP innych firm można importować z następujących formatów hello:  

- Przenośne kontener klucza symetrycznego (PSKC)  
- CSV, jeśli plik hello zawiera numer seryjny, klucz tajny w formacie Base-32 i przedział czasu  

**Pytanie: czy za pomocą usług terminalowych toosecure serwera usługi Azure Multi-Factor Authentication?**

Tak, ale jeśli używasz systemu Windows Server 2012 R2 lub później tylko zabezpieczania usług terminalowych przy użyciu bramy usług pulpitu zdalnego (RD Gateway).

Zmiany zabezpieczeń w systemie Windows Server 2012 R2 zmienić sposób serwera usługi Azure Multi-Factor Authentication nawiąże połączenie toohello pakiet zabezpieczeń urzędu zabezpieczeń lokalnych (LSA) w systemie Windows Server 2012 i starszych wersji. W przypadku wersji usług terminalowych w systemie Windows Server 2012 lub starszym, możesz [zabezpieczenia aplikacji przy użyciu uwierzytelniania systemu Windows](multi-factor-authentication-get-started-server-windows.md#to-secure-an-application-with-windows-authentication-use-the-following-procedure). Jeśli korzystasz z systemu Windows Server 2012 R2, należy bramy usług pulpitu zdalnego.

**Pytanie: czy mogę skonfigurować identyfikator wywołującego na serwerze usługi MFA, ale Moi użytkownicy nadal otrzymywać połączeń usługi Multi-Factor Authentication anonimowego obiektu wywołującego.**

Podczas wywoływania usługi Multi-Factor Authentication za pośrednictwem hello publicznej sieci telefonicznej, czasami routingu operatora, który nie obsługuje identyfikatora obiektu wywołującego. W związku z tym identyfikator wywołującego nie jest gwarantowana, mimo że zawsze wysyła hello system Multi-Factor Authentication.

**Pytanie: Dlaczego Moi użytkownicy są tooregister zostanie wyświetlony monit o ich informacji o zabezpieczeniach?**
Istnieje kilka przyczyn, dla którego użytkowników może być tooregister zostanie wyświetlony monit o ich informacji o zabezpieczeniach:

- Użytkownik Hello została włączona dla usługi MFA przez administratora w usłudze Azure AD, ale nie ma informacji o zabezpieczeniach jeszcze zarejestrowana dla swojego konta.
- Witaj użytkownika została włączona dla własnym resetowania haseł w usłudze Azure AD. informacje o zabezpieczeniach Hello pomoże je zresetować swoje hasło w przyszłości hello one kiedykolwiek pamięta.
- Użytkownik Hello dostęp do aplikacji, która ma toorequire zasad dostępu warunkowego usługi MFA i nie wcześniej zarejestrowane w usłudze MFA.
- Hello użytkownik rejestruje urządzenia z usługą Azure AD (w tym Azure AD Join), organizacja wymaga usługi MFA dla rejestracji urządzeń, a użytkownik hello nie został wcześniej zarejestrowany dla usługi MFA.
- Witaj użytkownik generuje Windows Hello dla firm w systemie Windows 10, (które wymagają usługi MFA) i nie wcześniej zarejestrowane w usłudze MFA.
- Witaj organizacja ma utworzone i włączone zasady rejestracji usługi MFA, która została zastosowana toohello użytkownika.
- Użytkownik Hello wcześniej zarejestrowane w usłudze MFA, ale wybrano metodę weryfikacji, ponieważ wyłączonego administrator. Użytkownik Hello w związku z tym musi przechodzić przez rejestracji usługi MFA ponownie tooselect nowe domyślną metodę weryfikacji.


## <a name="errors"></a>Błędy
**Pytanie: co należy zrobić użytkownicy, jeśli wyświetlany jest komunikat "żądanie uwierzytelnienia nie jest dotyczy uaktywnionego konta", używając powiadomienia z aplikacji mobilnej?**

Poinformuj ich toofollow tooremove tej procedury konto za pomocą aplikacji mobilnej hello, następnie dodaj go ponownie:

1. Przejdź za[profilu portalu Azure](https://account.activedirectory.windowsazure.com/profile/) i zaloguj się przy użyciu konta organizacyjnego.
2. Wybierz **dodatkowej weryfikacji zabezpieczeń**.
3. Usuń istniejące konto hello z hello aplikacji mobilnej.
4. Kliknij przycisk **Konfiguruj**, a następnie postępuj zgodnie z aplikacji mobilnej tooreconfigure hello hello instrukcje.

**Pytanie: co należy zrobić użytkownicy, jeśli widzą komunikat o błędzie 0x800434D4L podczas rejestrowania się w aplikacji korzystających z przeglądarki tooa?**

Witaj 0x800434D4L błędu podczas próby toosign w tooa aplikacji korzystających z przeglądarki zainstalowane na komputerze lokalnym, który nie działa z konta, które wymagają weryfikacji dwuetapowej.

Obejście tego błędu jest kont użytkowników oddzielnych toohave dla administratora dotyczące i operacje bez uprawnień administratora. Później możesz połączyć skrzynek pocztowych między konta administratora i konta bez uprawnień administratora, aby móc zalogować się w tooOutlook przy użyciu konta bez uprawnień administratora. Aby uzyskać więcej informacji o tym rozwiązaniu, Dowiedz się, jak za[dawać możliwości tooopen i widoku hello zawartość skrzynki pocztowej użytkownika hello administratora](http://help.outlook.com/141/gg709759.aspx?sl=1).

## <a name="next-steps"></a>Następne kroki
Jeśli nie jest tutaj odpowiedzi na pytanie, pozostaw tę wartość w hello komentarze u dołu hello hello strony. Lub, poniżej przedstawiono kilka dodatkowych opcji uzyskiwanie pomocy:

* Wyszukiwanie hello [wiedzy pomocy technicznej firmy Microsoft](https://www.microsoft.com/en-us/Search/result.aspx?form=mssupport&q=phonefactor&form=mssupport) problemów technicznych toocommon rozwiązania.
* Wyszukaj i Przeglądaj pytania i odpowiedzi od społeczności hello lub zadać pytanie w hello [fora usługi Azure Active Directory](https://social.msdn.microsoft.com/Forums/azure/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).
* Jeśli jesteś starszej wersji klienta PhoneFactor i masz pytania lub potrzebujesz pomocy resetowania hasła, użyj hello [resetowania hasła](mailto:phonefactorsupport@microsoft.com) link tooopen sprawy pomocy technicznej.
* Skontaktuj się z pracownikiem pomocy technicznej za pośrednictwem [obsługi serwera usługi Azure Multi-Factor Authentication (PhoneFactor)](https://support.microsoft.com/oas/default.aspx?prid=14947). Podczas kontaktowania się z nami, jest przydatne, jeśli te informacje mogą obejmować o problem jak to możliwe. Informacje, które można podać obejmują hello strony, gdy był wyświetlany błąd hello, hello określonego kodu błędu, identyfikator określonej sesji hello i identyfikator hello hello użytkownika, który był wyświetlany błąd hello.
