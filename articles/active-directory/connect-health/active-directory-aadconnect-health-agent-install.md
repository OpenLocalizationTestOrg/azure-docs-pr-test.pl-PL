---
title: Instalacja agenta Connect Health aaaAzure AD | Dokumentacja firmy Microsoft
description: "Jest to strona hello Azure AD Connect Health, opisujący hello instalacji agenta usług AD FS i synchronizacji."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 1cc8ae90-607d-4925-9c30-6770a4bd1b4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9019628ec1d4c477496e08910cfd668ed1933a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-agent-installation"></a>Instalowanie agenta programu Azure AD Connect Health
Ten dokument przeprowadzi Cię przez proces instalowania i konfigurowania agentów hello Azure AD Connect Health. Możesz pobrać hello agentów z [tutaj](active-directory-aadconnect-health.md#download-and-install-azure-ad-connect-health-agent).

## <a name="requirements"></a>Wymagania
Witaj w poniższej tabeli znajduje się lista wymagań dotyczących korzystania z usługi Azure AD Connect Health.

| Wymaganie | Opis |
| --- | --- |
| Usługa Azure AD — wersja Premium |Azure AD Connect Health to funkcja usługi Azure AD w wersji Premium, dlatego wymaga tej usługi. </br></br>Aby uzyskać więcej informacji, zobacz [Getting started with Azure AD Premium](../active-directory-get-started-premium.md) (Wprowadzenie do usługi Azure AD w wersji Premium). </br>toostart bezpłatnej 30-dniowej wersji próbnej, zobacz [uruchomić wersję próbną.](https://azure.microsoft.com/trial/get-started-active-directory/) |
| Musi być globalnym administratorem Twojej tooget usługi Azure AD wprowadzenie do usługi Azure AD Connect Health |Domyślnie tylko administratorzy globalni hello można zainstalować i skonfigurować hello kondycji agentów tooget pracę, dostęp do portalu hello i wykonywać dowolne operacje w Azure AD Connect Health. Aby więcej informacji, zobacz [Administering your Azure AD directory](../active-directory-administer.md) (Administrowanie katalogiem usługi Azure AD). <br><br> Przy użyciu kontroli dostępu opartej na rolach można zezwolić na dostęp tooAzure AD Connect Health tooother użytkowników w organizacji. Aby uzyskać więcej informacji, zobacz [Role Based Access Control for Azure AD Connect Health](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) (Kontrola dostępu oparta na rolach dla programu Azure AD Connect Health). </br></br>**Ważne:** hello konto używane do instalowania agentów hello musi być konta firmowego lub szkolnego. Nie może być kontem Microsoft. Aby uzyskać więcej informacji, zobacz [Tworzenie konta na platformie Azure jako organizacja](../sign-up-organization.md) |
| Na każdym serwerze docelowym jest zainstalowany agent programu Azure AD Connect Health | Azure AD Connect Health wymaga toobe agentów kondycji hello zainstalowane i skonfigurowane na serwerach docelowych tooreceive hello danych i zapewnienia możliwości monitorowania i analizy hello </br></br>Na przykład tooget dane z infrastruktury usług AD FS, hello agent musi być zainstalowany na hello usług AD FS i serwery Proxy aplikacji sieci Web. Podobnie, tooget danych na lokalnej infrastruktury usług AD DS, musi być zainstalowany hello agent na kontrolerach domeny hello. </br></br> |
| Punktami końcowymi usług Azure toohello łączność wychodząca | Podczas instalacji i środowiska uruchomieniowego hello agent wymaga łączności tooAzure AD Connect Health — punkty końcowe usługi. Łączność wychodząca jest zablokowane, za pomocą zapory, upewnij się, że hello następujące punkty końcowe są dodawane toohello listy dozwolonych: </br></br><li>&#42;.blob.core.windows.net </li><li>&#42;.servicebus.windows.net — Port: 5671 </li><li>&#42;.adhybridhealth.azure.com/</li><li>https://management.azure.com </li><li>https://policykeyservice.dc.ad.msft.net/</li><li>https://login.windows.net</li><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li> |
|Łączność wychodząca na podstawie adresów IP | Dla adresu IP na podstawie adresu filtrowania na zaporach, można znaleźć toohello [zakresów adresów IP Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653).|
| Inspekcja połączenia SSL dla ruchu wychodzącego jest filtrowana lub wyłączona | Hello agenta rejestracji krok lub danych operacji przekazywania może zakończyć się niepowodzeniem w przypadku inspekcji SSL lub zakończenia dla ruchu wychodzącego w warstwie sieci hello. |
| Porty zapory na powitania serwera z systemem hello agenta. |Hello agent wymaga hello następujące porty zapory toobe otwarcia hello toocommunicate agenta z punktów końcowych usługi Azure AD Health hello.</br></br><li>Port TCP 443</li><li>Port TCP 5671</li> |
| Zezwalaj na powitania po witryn sieci Web, jeśli są włączone zwiększone zabezpieczenia programu Internet Explorer |Po włączeniu zwiększonych zabezpieczeń programu Internet Explorer, następnie hello następujące witryny sieci Web należy zezwolić na powitania serwera, który jest zainstalowany agent hello toohave będzie.</br></br><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li><li>https://login.windows.net</li><li>Serwer federacyjny Hello Twojej organizacji zaufany przez usługę Azure Active Directory. Na przykład: https://sts.contoso.com</li> |
|Wyłącz standard FIPS|Standard FIPS nie jest obsługiwany przez agentów programu Azure AD Connect Health.|

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-fs"></a>Instalowanie hello Agent Azure AD Connect Health dla usług AD FS
toostart hello instalacji agenta, kliknij dwukrotnie pobrany plik .exe hello. Na pierwszym ekranie powitania kliknij przycisk Instaluj.

![Weryfikowanie programu Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install1.png)

Po zakończeniu instalacji powitania kliknij przycisk Konfiguruj teraz.

![Weryfikowanie programu Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install2.png)

Spowoduje to uruchomienie procesu programu PowerShell okna tooinitiate hello agenta rejestracji. Po wyświetleniu monitu zaloguj się przy użyciu konta usługi Azure AD, które ma dostęp tooperform agenta rejestracji. Domyślnie hello konta administratora globalnego ma dostęp.

![Weryfikowanie programu Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install3.png)

Po zalogowaniu się działanie programu PowerShell będzie kontynuowane. Po zakończeniu instalacji można zamknąć środowiska PowerShell i hello konfiguracja została ukończona.

W tym momencie hello agent usługi powinny być uruchomiony automatycznie co hello agenta przekazywania hello wymagane dane toohello usługi w chmurze w bezpieczny sposób.

Jeśli nie zostały spełnione wszystkie wymagania wstępne hello opisane w poprzednich sekcjach hello, w oknie programu PowerShell hello są wyświetlane ostrzeżenia. Należy się hello toocomplete [wymagania](active-directory-aadconnect-health-agent-install.md#requirements) przed zainstalowaniem agenta hello. Witaj następującego zrzutu ekranu jest przykładem te błędy.

![Weryfikowanie programu Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install4.png)

tooverify hello agent został zainstalowany, poszukaj hello następujące usługi na powitania serwera. Jeśli ukończono konfiguracji hello one już powinna być uruchomiona. W przeciwnym wypadku te aplikacje zostały zatrzymane do czasu ukończenia konfiguracji hello.

* Usługa diagnostyczna usług AD FS programu Azure AD Connect Health
* Usługa szczegółowych informacji usług AD FS programu Azure AD Connect Health
* Usługa monitorowania usług AD FS programu Azure AD Connect Health

![Weryfikowanie programu Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install5.png)

### <a name="agent-installation-on-windows-server-2008-r2-servers"></a>Instalowanie agenta na serwerach z systemem Windows Server 2008 R2
Kroki dotyczące serwerów z systemem Windows Server 2008 R2:

1. Upewnij się, że ten serwer hello jest uruchomiony w dodatku Service Pack 1 lub nowszym.
2. Wyłącz zwiększone zabezpieczenia programu Internet Explorer, aby zainstalować agenta:
3. Instalowanie programu Windows PowerShell 4.0 na wszystkich serwerach hello wcześniejsze instalowanie hello agenta programu AD Health. tooinstall programu Windows PowerShell 4.0:
   * Zainstaluj [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=40779) przy użyciu powitania po Instalatora w trybie offline hello toodownload łącza.
   * Zainstaluj aplikację PowerShell ISE (z funkcji systemu Windows).
   * Zainstaluj hello [Windows Management Framework 4.0.](https://www.microsoft.com/download/details.aspx?id=40855)
   * Zainstaluj program Internet Explorer w wersji 10 lub nowszej na powitania serwera. (Wymaganego przez tooauthenticate usługi kondycji hello, przy użyciu poświadczeń administratora platformy Azure).
4. Aby uzyskać więcej informacji na temat instalowania programu Windows PowerShell 4.0 w systemie Windows Server 2008 R2, zobacz artykuł typu wiki hello [tutaj](http://social.technet.microsoft.com/wiki/contents/articles/20623.step-by-step-upgrading-the-powershell-version-4-on-2008-r2.aspx).

### <a name="enable-auditing-for-ad-fs"></a>Włączanie inspekcji dla usług AD FS
> [!NOTE]
> Ta sekcja dotyczy tylko serwerów tooAD FS. Nie masz toofollow te kroki dla serwerów Proxy aplikacji sieci Web hello.
>

Aby hello analizy użycia funkcji toogather i analizowanie danych, hello Azure AD Connect Health agent wymaga hello informacji w dziennikach inspekcji hello AD FS. Dzienniki te nie są domyślnie włączone. Hello Użyj następujących procedur tooenable AD FS inspekcji i hello toolocate usług AD FS inspekcji dzienniki na serwerach usług AD FS.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2008-r2"></a>tooenable inspekcji usług AD FS w systemie Windows Server 2008 R2
1. Kliknij przycisk **Start**, punktu zbyt**programy**, punktu zbyt**narzędzia administracyjne**, a następnie kliknij przycisk **zasady zabezpieczeń lokalnych**.
2. Przejdź toohello **zabezpieczeń Ustawienia zabezpieczeń\Zasady Lokalne\zarządzanie prawami** folder, a następnie kliknij dwukrotnie pozycję Generuj inspekcje zabezpieczeń.
3. Na powitania **Ustawianie zabezpieczeń lokalnych** karcie, sprawdź, czy jest wymienione konto usługi hello AD FS 2.0. Jeśli nie jest obecny, kliknij przycisk **Dodaj użytkownika lub grupę** i dodać go toohello listy, a następnie kliknij przycisk **OK**.
4. tooenable inspekcji, otwórz wiersz polecenia z podwyższonym poziomem uprawnień i uruchom następujące polecenie hello:<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable</code>
5. Zamknij przystawkę Zasady zabezpieczeń lokalnych, a następnie otwórz przystawkę Zarządzanie hello. hello tooopen przystawki Zarządzanie, kliknij przycisk **Start**, punktu zbyt**programy**, punktu zbyt**narzędzia administracyjne**, a następnie kliknij przycisk AD FS 2.0 zarządzania.
6. W okienku Akcje hello kliknij przycisk Edytuj właściwości usługi federacyjnej.
7. W hello **właściwości usługi federacyjnej** okna dialogowego kliknij hello **zdarzenia** kartę.
8. Wybierz hello **inspekcje zakończone sukcesem** i **inspekcje zakończone niepowodzeniem** pola wyboru.
9. Kliknij przycisk **OK**.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2012-r2"></a>tooenable inspekcji usług AD FS w systemie Windows Server 2012 R2
1. Otwórz **zasady zabezpieczeń lokalnych** otwierając **Menedżera serwera** na ekranie startowym hello lub Menedżera serwera na powitania zadań na pulpicie hello, następnie kliknij przycisk **narzędzia/Zasady zabezpieczeń lokalnych**.
2. Przejdź toohello **zabezpieczeń zabezpieczeń\Zasady Lokalne\przypisywanie praw** folder, a następnie kliknij dwukrotnie plik **Generuj inspekcje zabezpieczeń**.
3. Na powitania **Ustawianie zabezpieczeń lokalnych** karcie, sprawdź, czy jest wymienione konto usługi hello AD FS. Jeśli nie jest obecny, kliknij przycisk **Dodaj użytkownika lub grupę** i dodać go toohello listy, a następnie kliknij przycisk **OK**.
4. Inspekcja tooenable, otwórz wiersz polecenia z podwyższonym poziomem uprawnień i uruchom następujące polecenie hello: ```auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable```.
5. Zamknij **zasady zabezpieczeń lokalnych**, a następnie otwórz hello **Zarządzanie usługami AD FS** przystawki (w Menedżerze serwera kliknij pozycję Narzędzia, a następnie wybierz Zarządzanie usługami AD FS).
6. W okienku Akcje powitania kliknij **Edytuj właściwości usługi federacyjnej**.
7. Okno dialogowe właściwości usługi federacyjnej hello, kliknij przycisk hello **zdarzenia** kartę.
8. Wybierz hello **inspekcje zakończone sukcesem i inspekcje zakończone niepowodzeniem** pola wyboru, a następnie kliknij przycisk **OK**.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2016"></a>tooenable inspekcji usług AD FS w systemie Windows Server 2016
1. Otwórz **zasady zabezpieczeń lokalnych** otwierając **Menedżera serwera** na ekranie startowym hello lub Menedżera serwera na powitania zadań na pulpicie hello, następnie kliknij przycisk **narzędzia/Zasady zabezpieczeń lokalnych**.
2. Przejdź toohello **zabezpieczeń zabezpieczeń\Zasady Lokalne\przypisywanie praw** folder, a następnie kliknij dwukrotnie plik **Generuj inspekcje zabezpieczeń**.
3. Na powitania **Ustawianie zabezpieczeń lokalnych** karcie, sprawdź, czy jest wymienione konto usługi hello AD FS. Jeśli nie jest obecny, kliknij przycisk **Dodaj użytkownika lub grupę** i dodać hello AD FS usługi konta toohello listy, a następnie kliknij przycisk **OK**.
4. tooenable inspekcji, otwórz wiersz polecenia z podwyższonym poziomem uprawnień i uruchom następujące polecenie hello:<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable.</code>
5. Zamknij **zasady zabezpieczeń lokalnych**, a następnie otwórz hello **Zarządzanie usługami AD FS** przystawki (w Menedżerze serwera kliknij pozycję Narzędzia, a następnie wybierz Zarządzanie usługami AD FS).
6. W okienku Akcje powitania kliknij **Edytuj właściwości usługi federacyjnej**.
7. Okno dialogowe właściwości usługi federacyjnej hello, kliknij przycisk hello **zdarzenia** kartę.
8. Wybierz hello **inspekcje zakończone sukcesem i inspekcje zakończone niepowodzeniem** pola wyboru, a następnie kliknij przycisk **OK**. Powinno to być włączone domyślnie.
9. Otwórz okno programu PowerShell i uruchom następujące polecenie hello: ```Set-AdfsProperties -AuditLevel Verbose```.

Zwróć uwagę, że poziom inspekcji „basic” (podstawowy) jest włączony domyślnie. Dowiedz się więcej o hello [ulepszenie AD FS inspekcji w systemie Windows Server 2016](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/operations/auditing-enhancements-to-ad-fs-in-windows-server-2016)


#### <a name="toolocate-hello-ad-fs-audit-logs"></a>Dzienniki inspekcji hello toolocate usług AD FS
1. Otwórz **Podgląd zdarzeń**.
2. Przejdź dzienniki tooWindows i wybierz polecenie **zabezpieczeń**.
3. W prawo hello, kliknij polecenie **Filtruj bieżące dzienniki**.
4. W obszarze Źródło zdarzenia wybierz pozycję **Inspekcja usług AD FS**.

![Dzienniki inspekcji usług AD FS](./media/active-directory-aadconnect-health-requirements/adfsaudit.png)

> [!WARNING]
> Zasady grupy mogą wyłączyć inspekcję usług AD FS. Jeśli inspekcja usług AD FS jest wyłączona, analiza użycia dotycząca aktywności logowania jest niedostępna. Upewnij się, że nie masz zasad grupy, które wyłączają inspekcję usług AD FS.>
>


## <a name="installing-hello-azure-ad-connect-health-agent-for-sync"></a>Instalowanie agenta hello Azure AD Connect Health do celów synchronizacji
agenta Hello Azure AD Connect Health do celów synchronizacji jest instalowany automatycznie w hello najnowszej kompilacji programu Azure AD Connect. toouse Azure AD Connect do celów synchronizacji, należy toodownload hello najnowszą wersję programu Azure AD Connect i zainstaluj go. Możesz pobrać najnowszą wersję hello [tutaj](http://www.microsoft.com/download/details.aspx?id=47594).

tooverify hello agent został zainstalowany, poszukaj hello następujące usługi na powitania serwera. Jeśli ukończono konfiguracji hello one już powinna być uruchomiona. W przeciwnym wypadku te aplikacje zostały zatrzymane do czasu ukończenia konfiguracji hello.

* Usługa szczegółowych informacji synchronizacji programu Azure AD Connect Health
* Usługa monitorowania synchronizacji programu Azure AD Connect Health

![Weryfikowanie programu Azure AD Connect Health do celów synchronizacji](./media/active-directory-aadconnect-health-sync/services.png)

> [!NOTE]
> Pamiętaj, że do korzystania z programu Azure AD Connect Health jest wymagana usługa Azure AD w wersji Premium. Jeśli nie masz usługi Azure AD Premium, to toocomplete hello konfiguracji w hello portalu Azure. Aby uzyskać więcej informacji, zobacz hello [strony wymagania](active-directory-aadconnect-health-agent-install.md#requirements).
>
>

## <a name="manual-azure-ad-connect-health-for-sync-registration"></a>Ręczne rejestrowanie programu Azure AD Connect Health do celów synchronizacji
Jeśli hello Azure AD Connect Health dla synchronizacji Rejestracja agenta nie powiedzie się po pomyślnym zainstalowaniu programu Azure AD Connect, możesz użyć następującego polecenia programu PowerShell toomanually zarejestrować agenta hello hello.

> [!IMPORTANT]
> Za pomocą tego polecenia programu PowerShell jest tylko wymagane, jeśli hello Rejestracja agenta nie powiedzie się po zainstalowaniu programu Azure AD Connect.
>
>

Witaj PowerShell następujące polecenie jest wymagany tylko jeśli rejestracja agenta kondycji hello nie powiedzie się nawet po pomyślnej instalacji i konfiguracji programu Azure AD Connect. usługi Azure AD Connect Health Hello zostanie uruchomione po hello agent został pomyślnie zarejestrowany.

Możesz ręcznie zarejestrować hello Azure AD Connect Health agent dla synchronizacji za pomocą następującego polecenia programu PowerShell hello:

`Register-AzureADConnectHealthSyncAgent -AttributeFiltering $false -StagingMode $false`

polecenie Hello przyjmuje następujące parametry:

* AttributeFiltering: $true (domyślnie) — Jeśli Azure AD Connect nie synchronizuje hello domyślnego zestawu atrybutów i został dostosowany toouse filtrowane atrybutu zestawu. W przeciwnym razie $false.
* StagingMode: $false (domyślnie) — Jeśli hello Azure AD Connect serwera nie jest w trybie przejściowym, $true Jeśli hello serwer jest skonfigurowany toobe w trybie przejściowym.

Po wyświetleniu monitu o uwierzytelniania należy używać tego samego konta administratora globalnego hello (takie jak admin@domain.onmicrosoft.com) użytego do konfigurowania usługi Azure AD Connect.

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-ds"></a>Instalowanie hello Agent Azure AD Connect Health dla usług AD DS
toostart hello instalacji agenta, kliknij dwukrotnie pobrany plik .exe hello. Na pierwszym ekranie powitania kliknij przycisk Instaluj.

![Weryfikowanie programu Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install1.png)

Po zakończeniu instalacji powitania kliknij przycisk Konfiguruj teraz.

![Weryfikowanie programu Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install2.png)

Zostanie uruchomiony wiersz polecenia, a następnie pewne polecenia programu PowerShell, które spowodują wykonanie polecenia Register-AzureADConnectHealthADDSAgent. Gdy zostanie wyświetlony monit o toosign w tooAzure, przejdź dalej i zaloguj się.

![Weryfikowanie programu Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install3.png)

Po zalogowaniu się działanie programu PowerShell będzie kontynuowane. Po zakończeniu instalacji można zamknąć środowiska PowerShell i hello konfiguracja została ukończona.

W tym momencie usługi hello powinna być uruchamiana automatycznie, dzięki czemu hello agenta toomonitor i zbierania danych. Jeśli nie zostały spełnione wszystkie wymagania wstępne hello opisane w poprzednich sekcjach hello, w oknie programu PowerShell hello są wyświetlane ostrzeżenia. Należy się hello toocomplete [wymagania](active-directory-aadconnect-health-agent-install.md#requirements) przed zainstalowaniem agenta hello. Witaj następującego zrzutu ekranu jest przykładem te błędy.

![Weryfikowanie programu Azure AD Connect Health dla usług AD DS](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install4.png)

tooverify hello agent został zainstalowany, poszukaj hello następujące usługi na kontrolerze domeny hello.

* Usługa szczegółowych informacji usług AD DS programu Azure AD Connect Health
* Usługa monitorowania usług AD DS programu Azure AD Connect Health

Jeśli ukończono hello konfiguracji tych usług powinna już działać. W przeciwnym wypadku te aplikacje zostały zatrzymane do czasu ukończenia konfiguracji hello.

![Weryfikowanie programu Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install5.png)


### <a name="agent-registration-using-powershell"></a>Rejestracja agenta przy użyciu programu PowerShell
Po zainstalowaniu hello odpowiedniego agenta setup.exe, można wykonać krok rejestracji agenta hello za pomocą następującego polecenia programu PowerShell w zależności od roli hello hello. Otwórz okno programu PowerShell, a następnie wykonaj odpowiednie polecenie hello:

```
    Register-AzureADConnectHealthADFSAgent
    Register-AzureADConnectHealthADDSAgent
    Register-AzureADConnectHealthSyncAgent

```

Te polecenia zaakceptować "Poświadczenia" jako parametru toocomplete hello rejestracja w sposób nieinterakcyjnym lub na komputerze, Server Core.
* Witaj poświadczeń, można przechwycić w zmiennej środowiska PowerShell, która została przekazana jako parametr.
* Możesz podać wszystkie usługi Azure AD Identity, który ma dostęp tooregister hello agentów i nie jest włączone uwierzytelnianie MFA.
* Domyślnie administratorzy globalni mają dostęp tooperform agenta rejestracji. Możesz również zezwolić innych mniej tooperform tożsamościami uprzywilejowanymi ten krok. Przeczytaj więcej na temat [kontroli dostępu na podstawie ról](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control).

```
    $cred = Get-Credential
    Register-AzureADConnectHealthADFSAgent -Credential $cred

```

## <a name="configure-azure-ad-connect-health-agents-toouse-http-proxy"></a>Konfigurowanie usługi Azure AD Connect agentów kondycji toouse serwer HTTP Proxy
Azure AD Connect agentów kondycji toowork można skonfigurować serwer HTTP Proxy.

> [!NOTE]
> * Za pomocą "Netsh WinHttp set ProxyServerAddress" nie jest obsługiwana, ponieważ hello agent używa żądań sieci web toomake System.Net zamiast usług Microsoft Windows HTTP Services.
> * Witaj skonfigurowany adres serwera Http Proxy jest używany przez toopass szyfrowanych komunikatów Https.
> * Uwierzytelniane (przy użyciu metody HTTPBasic) serwery proxy nie są obsługiwane.
>
>

### <a name="change-health-agent-proxy-configuration"></a>Zmienianie konfiguracji serwera proxy agenta kondycji
Masz hello następujące opcje tooconfigure usługi Azure AD Connect Agent kondycji toouse serwer HTTP Proxy.

> [!NOTE]
> Wszystkie usługi Azure AD Connect Agent kondycji należy ponownie uruchomić, aby toobe ustawienia serwera proxy hello zaktualizowane. Uruchom następujące polecenie hello:<br>
> Restart-Service AdHealth*
>
>

#### <a name="import-existing-proxy-settings"></a>Importowanie istniejących ustawień serwera proxy
##### <a name="import-from-internet-explorer"></a>Importowanie z programu Internet Explorer
Nie można zaimportować ustawienia serwera proxy programu Internet Explorer HTTP, toobe używane przez hello Azure agentów AD Connect Health. Na wszystkich serwerach hello, w którym jest uruchomiony agent kondycji hello wykonaj następujące polecenia programu PowerShell hello:

    Set-AzureAdConnectHealthProxySettings -ImportFromInternetSettings

##### <a name="import-from-winhttp"></a>Importowanie z usług WinHTTP
Nie można zaimportować ustawienia serwera proxy WinHTTP, toobe używane przez hello Azure agentów AD Connect Health. Na wszystkich serwerach hello, w którym jest uruchomiony agent kondycji hello wykonaj następujące polecenia programu PowerShell hello:

    Set-AzureAdConnectHealthProxySettings -ImportFromWinHttp

#### <a name="specify-proxy-addresses-manually"></a>Ręczne określanie adresów serwerów proxy
Serwer proxy można ręcznie określić na wszystkich serwerach hello uruchomiony Agent kondycji hello, wykonując następujące polecenia programu PowerShell hello:

    Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress address:port

Przykład: *Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress mojserwerproxy: 443*

* Parametr „address” może być rozpoznawalną nazwą serwera w systemie DNS lub adresem IPv4.
* Parametr „port” można pominąć. W przypadku pominięcia jako domyślny zostanie wybrany port 443.

#### <a name="clear-existing-proxy-configuration"></a>Czyszczenie istniejącej konfiguracji serwera proxy
Hello istniejącą konfigurację serwera proxy możesz wyczyścić, uruchamiając następujące polecenie hello:

    Set-AzureAdConnectHealthProxySettings -NoProxy


### <a name="read-current-proxy-settings"></a>Odczytywanie bieżących ustawień serwera proxy
Możesz przeczytać hello aktualnie skonfigurowanych ustawień serwera proxy, uruchamiając następujące polecenie hello:

    Get-AzureAdConnectHealthProxySettings


## <a name="test-connectivity-tooazure-ad-connect-health-service"></a>Testowanie łączności tooAzure AD Connect usługi kondycji
Istnieje możliwość, że może spowodować problemy powodujące hello Azure AD Connect Health agent toolose łączności z hello Azure AD Connect Health service. Ich przyczyną mogą być problemy z siecią, problemy z uprawnieniami lub różne inne czynniki.

Jeśli hello agent usługi toosend danych toohello usługi Azure AD Connect Health przez ponad dwie godziny, wskazane jest z następującego alertu w portalu hello hello: "dane usługi kondycji nie jest zapasowej toodate." Można potwierdzić, czy wpływ hello Azure AD Connect Health agent jest stanie tooupload danych toohello usługi Azure AD Connect Health service, uruchamiając następujące polecenia programu PowerShell hello:

    Test-AzureADConnectHealthConnectivity -Role ADFS

Witaj parametr roli obecnie przyjmuje hello następujące wartości:

* ADFS
* Sync
* ADDS

Można użyć flagi - ShowResults hello w tooview polecenia hello szczegółowe dzienniki. Poniższy przykład hello użycia:

    Test-AzureADConnectHealthConnectivity -Role Sync -ShowResult

> [!NOTE]
> narzędzie łączności hello toouse, należy pierwszej pełną hello agenta rejestracji. Jeśli nie jest możliwe toocomplete hello agenta rejestracji, upewnij się, że spełniono wszystkie hello [wymagania](active-directory-aadconnect-health-agent-install.md#requirements) dla usługi Azure AD Connect Health. Ten test łączności jest wykonywany domyślnie podczas rejestracji agenta.
>
>

## <a name="related-links"></a>Powiązane linki
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Operacje w programie Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Używanie programu Azure AD Connect Health z usługami AD FS](active-directory-aadconnect-health-adfs.md)
* [Używanie programu Azure AD Connect Health w celu synchronizacji](active-directory-aadconnect-health-sync.md)
* [Używanie programu Azure AD Connect Health z usługami AD DS](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health — często zadawane pytania](active-directory-aadconnect-health-faq.md)
* [Historia wersji programu Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
