---
title: Instalacja agenta programu Azure AD Connect Health | Microsoft Docs
description: "Jest to strona programu Azure AD Connect Health opisująca instalację agenta usług AD FS i synchronizacji."
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
ms.openlocfilehash: 8ef8a1cc2393f0befbf83c3124b67b405ae06898
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-health-agent-installation"></a>Instalowanie agenta programu Azure AD Connect Health
W tym dokumencie opisano instalowanie i konfigurowanie agentów programu Azure AD Connect Health. Agentów możesz pobrać [tutaj](active-directory-aadconnect-health.md#download-and-install-azure-ad-connect-health-agent).

## <a name="requirements"></a>Wymagania
Poniższa tabela zawiera listę wymagań dotyczących używania programu Azure AD Connect Health.

| Wymaganie | Opis |
| --- | --- |
| Usługa Azure AD — wersja Premium |Azure AD Connect Health to funkcja usługi Azure AD w wersji Premium, dlatego wymaga tej usługi. </br></br>Aby uzyskać więcej informacji, zobacz [Getting started with Azure AD Premium](../active-directory-get-started-premium.md) (Wprowadzenie do usługi Azure AD w wersji Premium). </br>Aby skorzystać z bezpłatnej 30-dniowej wersji próbnej, zobacz [Włączanie wersji próbnej](https://azure.microsoft.com/trial/get-started-active-directory/). |
| Aby rozpocząć pracę z programem Azure AD Connect Health, musisz być administratorem globalnym usługi Azure AD |Domyślnie tylko administratorzy globalni mogą instalować i konfigurować agentów kondycji, aby rozpoczynać pracę z programem Azure AD Connect Health, uzyskiwać dostęp do portalu i wykonywać dowolne operacje w programie. Aby więcej informacji, zobacz [Administering your Azure AD directory](../active-directory-administer.md) (Administrowanie katalogiem usługi Azure AD). <br><br> Używając funkcji kontroli dostępu opartej na rolach, możesz zezwalać na dostęp do programu Azure AD Connect Health innym użytkownikom w organizacji. Aby uzyskać więcej informacji, zobacz [Role Based Access Control for Azure AD Connect Health](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) (Kontrola dostępu oparta na rolach dla programu Azure AD Connect Health). </br></br>**Ważne:** Konto używane podczas instalowania agentów musi być kontem służbowym. Nie może być kontem Microsoft. Aby uzyskać więcej informacji, zobacz [Tworzenie konta na platformie Azure jako organizacja](../sign-up-organization.md) |
| Na każdym serwerze docelowym jest zainstalowany agent programu Azure AD Connect Health | Program Azure AD Connect Health wymaga zainstalowania i skonfigurowania agentów kondycji na serwerach docelowych w celu odbioru danych i zapewniania możliwości monitorowania i analizy </br></br>Na przykład aby uzyskać dane z infrastruktury usług AD FS, musisz zainstalować agenta na serwerach proxy usług AD FS i aplikacji sieci Web. Podobnie, aby uzyskać dane dotyczące lokalnej infrastruktury usług AD DS, agent musi być zainstalowany na kontrolerach domeny. </br></br> |
| Łączność wychodząca z punktami końcowymi usług Azure | Podczas instalowania i w czasie pracy agent wymaga łączności z punktami końcowymi usługi Azure AD Connect Health. Jeśli łączność wychodząca jest blokowana przy użyciu zapór, nie zapomnij dodać następujących punktów końcowych do listy lokalizacji dozwolonych: </br></br><li>&#42;.blob.core.windows.net </li><li>&#42;.servicebus.windows.net — Port: 5671 </li><li>&#42;.adhybridhealth.azure.com/</li><li>https://management.azure.com </li><li>https://policykeyservice.dc.ad.msft.net/</li><li>https://login.windows.net</li><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li> |
|Łączność wychodząca na podstawie adresów IP | W przypadku filtrowania zapory opartego na adresach IP zapoznaj się z [zakresem adresów IP platformy Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653).|
| Inspekcja połączenia SSL dla ruchu wychodzącego jest filtrowana lub wyłączona | Rejestracja agenta lub operacje przekazywania danych mogą zakończyć się niepowodzeniem, jeśli w warstwie sieciowej jest aktywny proces zakończenia lub inspekcji połączenia SSL dla ruchu wychodzącego. |
| Porty zapory na serwerze, na którym jest uruchomiony agent |Agent wymaga, aby poniższe porty zapory były otwarte w celu komunikacji z punktami końcowymi usług programu Azure AD Connect Health.</br></br><li>Port TCP 443</li><li>Port TCP 5671</li> |
| Zezwalaj na następujące witryny sieci web, jeśli są włączone zwiększone zabezpieczenia programu Internet Explorer |Jeśli zwiększone zabezpieczenia programu Internet Explorer są włączone na serwerze, na którym ma zostać zainstalowany agent, musisz zezwolić na otwieranie poniższych witryn sieci Web.</br></br><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li><li>https://login.windows.net</li><li>Serwer federacyjny Twojej organizacji zaufany przez usługę Azure Active Directory. Na przykład: https://sts.contoso.com</li> |
|Wyłącz standard FIPS|Standard FIPS nie jest obsługiwany przez agentów programu Azure AD Connect Health.|

## <a name="installing-the-azure-ad-connect-health-agent-for-ad-fs"></a>Instalowanie agenta programu Azure AD Connect Health Agent dla usług AD FS
Aby rozpocząć instalowanie agenta, kliknij dwukrotnie pobrany plik exe. Na pierwszym ekranie kliknij przycisk Instaluj.

![Weryfikowanie programu Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install1.png)

Po zakończeniu instalacji kliknij przycisk Konfiguruj teraz.

![Weryfikowanie programu Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install2.png)

Spowoduje to uruchomienie okna programu PowerShell w celu zainicjowania procesu rejestracji agenta. Po wyświetleniu monitu zaloguj się przy użyciu konta usługi Azure AD, które ma dostęp do przeprowadzenia rejestracji agenta. Taki dostęp ma domyślnie konto administratora globalnego.

![Weryfikowanie programu Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install3.png)

Po zalogowaniu się działanie programu PowerShell będzie kontynuowane. Gdy program PowerShell zakończy pracę, możesz go zamknąć. Konfiguracja zostanie zakończona.

Na tym etapie usługi agenta powinni zostać uruchomione automatyczne i zezwolić agentowi na bezpieczne przekazanie wymaganych danych do usługi w chmurze.

Jeśli nie zostały spełnione wszystkie wymagania wstępne, które zostały opisane w poprzednich sekcjach, w oknie programu PowerShell będą wyświetlane ostrzeżenia. Przed zainstalowaniem agenta upewnij się, że zostały spełnione [wymagania](active-directory-aadconnect-health-agent-install.md#requirements). Poniższy zrzut ekranu przedstawia przykład tego rodzaju błędów.

![Weryfikowanie programu Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install4.png)

Aby sprawdzić, czy agent został zainstalowany, znajdź następujące usługi na serwerze: Jeśli konfiguracja została zakończona, te usługi powinny być uruchomione. W przeciwnym razie pozostaną one zatrzymane do czasu zakończenia konfiguracji.

* Usługa diagnostyczna usług AD FS programu Azure AD Connect Health
* Usługa szczegółowych informacji usług AD FS programu Azure AD Connect Health
* Usługa monitorowania usług AD FS programu Azure AD Connect Health

![Weryfikowanie programu Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install5.png)

### <a name="agent-installation-on-windows-server-2008-r2-servers"></a>Instalowanie agenta na serwerach z systemem Windows Server 2008 R2
Kroki dotyczące serwerów z systemem Windows Server 2008 R2:

1. Upewnij się, że na serwerze jest uruchomiony system z dodatkiem Service Pack 1 lub nowszym.
2. Wyłącz zwiększone zabezpieczenia programu Internet Explorer, aby zainstalować agenta:
3. Zanim zainstalujesz agenta programu AD Connect Health, na każdym serwerze zainstaluj program Windows PowerShell 4.0. Aby zainstalować program Windows PowerShell 4.0:
   * Zainstaluj platformę [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=40779), używając poniższego linku w celu pobrania instalatora w trybie offline.
   * Zainstaluj aplikację PowerShell ISE (z funkcji systemu Windows).
   * Zainstaluj platformę [Windows Management Framework 4.0](https://www.microsoft.com/download/details.aspx?id=40855).
   * Zainstaluj na serwerze program Internet Explorer w wersji 10 lub nowszej. (Wymagane przez usługę kondycji do uwierzytelnienia przy użyciu poświadczeń administratora platformy Azure.)
4. Aby uzyskać więcej informacji na temat instalowania programu Windows PowerShell 4.0 w systemie Windows Server 2008 R2, zobacz artykuł w witrynie wiki [tutaj](http://social.technet.microsoft.com/wiki/contents/articles/20623.step-by-step-upgrading-the-powershell-version-4-on-2008-r2.aspx).

### <a name="enable-auditing-for-ad-fs"></a>Włączanie inspekcji dla usług AD FS
> [!NOTE]
> Informacje w tej sekcji dotyczą tylko serwerów usług AD FS. Nie musisz wykonywać tych instrukcji na serwerach proxy aplikacji sieci Web.
>

Aby funkcja Analiza użycia mogła zbierać i analizować dane, agent programu Azure AD Connect Health potrzebuje informacji zawartych w dziennikach inspekcji usług AD FS. Dzienniki te nie są domyślnie włączone. Do włączania inspekcji usług AD FS i lokalizowania dzienników inspekcji usług AD FS na własnych serwerach usług AD FS służą poniższe procedury.

#### <a name="to-enable-auditing-for-ad-fs-on-windows-server-2008-r2"></a>Aby włączyć inspekcję usług AD FS w systemie Windows Server 2008 R2
1. Kliknij przycisk **Start**, wskaż pozycję **Programy**, wskaż pozycję **Narzędzia administracyjne**, a następnie kliknij pozycję **Zasady zabezpieczeń lokalnych**.
2. Przejdź do folderu **Ustawienia zabezpieczeń\Zasady lokalne\Zarządzanie prawami użytkownika**, a następnie kliknij dwukrotnie pozycję Generuj inspekcje zabezpieczeń.
3. Na karcie **Ustawianie zabezpieczeń lokalnych** sprawdź, czy jest wymienione konto usługi AD FS 2.0. Jeśli go nie ma, kliknij pozycję **Dodaj użytkownika lub grupę** i dodaj je do listy, a następnie kliknij przycisk **OK**.
4. Aby włączyć inspekcję, otwórz wiersz polecenia z podwyższonym poziomem uprawnień i uruchom następujące polecenie: <code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable</code>
5. Zamknij okno Zasady zabezpieczeń lokalnych, a następnie otwórz przystawkę Zarządzanie. Aby otworzyć przystawkę Zarządzanie, kliknij przycisk **Start**, wskaż pozycję **Programy**, wskaż pozycję **Narzędzia administracyjne**, a następnie kliknij pozycję Zarządzanie usługą AD FS 2.0.
6. W okienku Akcje kliknij pozycję Edytuj właściwości usługi federacyjnej.
7. W oknie dialogowym **Właściwości usługi federacyjnej** kliknij kartę **Zdarzenia**.
8. Zaznacz pola wyboru **Inspekcje zakończone sukcesem** i **Inspekcje zakończone niepowodzeniem**.
9. Kliknij przycisk **OK**.

#### <a name="to-enable-auditing-for-ad-fs-on-windows-server-2012-r2"></a>Aby włączyć inspekcję usług AD FS w systemie Windows Server 2012 R2
1. Otwórz okno **Zasady zabezpieczeń lokalnych**, klikając pozycję **Menedżer serwera** na ekranie startowym lub pasku zadań na pulpicie, a następnie kliknij pozycję **Narzędzia/Zasady zabezpieczeń lokalnych**.
2. Przejdź do folderu **Ustawienia zabezpieczeń\Zasady lokalne\Przypisywanie praw użytkownika**, a następnie kliknij dwukrotnie pozycję **Generuj inspekcje zabezpieczeń**.
3. Na karcie **Ustawianie zabezpieczeń lokalnych** sprawdź, czy jest wymienione konto usługi AD FS. Jeśli go nie ma, kliknij pozycję **Dodaj użytkownika lub grupę** i dodaj je do listy, a następnie kliknij przycisk **OK**.
4. Aby włączyć inspekcję, otwórz wiersz polecenia z podwyższonym poziomem uprawnień i uruchom następujące polecenie: ```auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable```.
5. Zamknij okno **Zasady zabezpieczeń lokalnych**, a następnie otwórz przystawkę **Zarządzanie usługami AD FS** (w Menedżerze serwera kliknij pozycję Narzędzia, a następnie wybierz pozycję Zarządzanie usługami AD FS).
6. W okienku Akcje kliknij pozycję **Edytuj właściwości usługi federacyjnej**.
7. W oknie dialogowym Właściwości usługi federacyjnej kliknij kartę **Zdarzenia**.
8. Zaznacz pola wyboru **Inspekcje zakończone sukcesem i Inspekcje zakończone niepowodzeniem**, a następnie kliknij przycisk **OK**.

#### <a name="to-enable-auditing-for-ad-fs-on-windows-server-2016"></a>Aby włączyć inspekcję usług AD FS w systemie Windows Server 2016
1. Otwórz okno **Zasady zabezpieczeń lokalnych**, klikając pozycję **Menedżer serwera** na ekranie startowym lub pasku zadań na pulpicie, a następnie kliknij pozycję **Narzędzia/Zasady zabezpieczeń lokalnych**.
2. Przejdź do folderu **Ustawienia zabezpieczeń\Zasady lokalne\Przypisywanie praw użytkownika**, a następnie kliknij dwukrotnie pozycję **Generuj inspekcje zabezpieczeń**.
3. Na karcie **Ustawianie zabezpieczeń lokalnych** sprawdź, czy jest wymienione konto usługi AD FS. Jeśli go nie ma, kliknij pozycję **Dodaj użytkownika lub grupę** i dodaj konto usług AD FS do listy, a następnie kliknij przycisk **OK**.
4. Aby włączyć inspekcję, otwórz wiersz polecenia z podwyższonym poziomem uprawnień i uruchom następujące polecenie: <code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable.</code>
5. Zamknij okno **Zasady zabezpieczeń lokalnych**, a następnie otwórz przystawkę **Zarządzanie usługami AD FS** (w Menedżerze serwera kliknij pozycję Narzędzia, a następnie wybierz pozycję Zarządzanie usługami AD FS).
6. W okienku Akcje kliknij pozycję **Edytuj właściwości usługi federacyjnej**.
7. W oknie dialogowym Właściwości usługi federacyjnej kliknij kartę **Zdarzenia**.
8. Zaznacz pola wyboru **Inspekcje zakończone sukcesem i Inspekcje zakończone niepowodzeniem**, a następnie kliknij przycisk **OK**. Powinno to być włączone domyślnie.
9. Otwórz okno programu PowerShell i uruchom następujące polecenie: ```Set-AdfsProperties -AuditLevel Verbose```.

Zwróć uwagę, że poziom inspekcji „basic” (podstawowy) jest włączony domyślnie. Przeczytaj więcej na temat [ulepszenia inspekcji usług AD FS w systemie Windows Server 2016](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/operations/auditing-enhancements-to-ad-fs-in-windows-server-2016)


#### <a name="to-locate-the-ad-fs-audit-logs"></a>Aby zlokalizować dzienniki inspekcji usług AD FS
1. Otwórz **Podgląd zdarzeń**.
2. Przejdź do dzienników systemu Windows i wybierz pozycję **Zabezpieczenia**.
3. Po prawej stronie kliknij pozycję **Filtruj bieżące dzienniki**.
4. W obszarze Źródło zdarzenia wybierz pozycję **Inspekcja usług AD FS**.

![Dzienniki inspekcji usług AD FS](./media/active-directory-aadconnect-health-requirements/adfsaudit.png)

> [!WARNING]
> Zasady grupy mogą wyłączyć inspekcję usług AD FS. Jeśli inspekcja usług AD FS jest wyłączona, analiza użycia dotycząca aktywności logowania jest niedostępna. Upewnij się, że nie masz zasad grupy, które wyłączają inspekcję usług AD FS.>
>


## <a name="installing-the-azure-ad-connect-health-agent-for-sync"></a>Instalowanie agenta programu Azure AD Connect Health do celów synchronizacji
W najnowszej kompilacji programu Azure AD Connect agent programu Azure AD Connect Health do celów synchronizacji jest instalowany automatycznie. Aby używać programu Azure AD Connect do celów synchronizacji, musisz pobrać i zainstalować najnowszą wersję programu Azure AD Connect. Najnowszą wersję możesz pobrać [tutaj](http://www.microsoft.com/download/details.aspx?id=47594).

Aby sprawdzić, czy agent został zainstalowany, znajdź następujące usługi na serwerze: Jeśli konfiguracja została zakończona, te usługi powinny być uruchomione. W przeciwnym razie pozostaną one zatrzymane do czasu zakończenia konfiguracji.

* Usługa szczegółowych informacji synchronizacji programu Azure AD Connect Health
* Usługa monitorowania synchronizacji programu Azure AD Connect Health

![Weryfikowanie programu Azure AD Connect Health do celów synchronizacji](./media/active-directory-aadconnect-health-sync/services.png)

> [!NOTE]
> Pamiętaj, że do korzystania z programu Azure AD Connect Health jest wymagana usługa Azure AD w wersji Premium. Jeśli nie masz usługi Azure AD w wersji Premium, nie możesz ukończyć konfiguracji w witrynie Azure Portal. Aby uzyskać więcej informacji, zobacz [stronę wymagań](active-directory-aadconnect-health-agent-install.md#requirements).
>
>

## <a name="manual-azure-ad-connect-health-for-sync-registration"></a>Ręczne rejestrowanie programu Azure AD Connect Health do celów synchronizacji
Jeśli rejestracja agenta programu Azure AD Connect Health do celów synchronizacji nie powiedzie się po pomyślnym zainstalowaniu programu Azure AD Connect, możesz użyć poniższego polecenia programu PowerShell, aby ręcznie zarejestrować agenta.

> [!IMPORTANT]
> Użycie tego polecenia programu PowerShell jest wymagane tylko wtedy, gdy rejestracja agenta nie powiedzie się po zainstalowaniu programu Azure AD Connect.
>
>

Poniższe polecenie programu PowerShell jest wymagane TYLKO w przypadku, gdy rejestracja agenta kondycji zakończy się niepowodzeniem nawet po pomyślnym zainstalowaniu i skonfigurowaniu programu Azure AD Connect. Usługi programu Azure AD Connect Health zostaną uruchomione po pomyślnym zarejestrowaniu agenta.

Agenta programu Azure AD Connect Health do celów synchronizacji możesz zarejestrować ręcznie, używając następującego polecenia programu PowerShell:

`Register-AzureADConnectHealthSyncAgent -AttributeFiltering $false -StagingMode $false`

Polecenie przyjmuje następujące parametry:

* AttributeFiltering: $true (domyślnie) — jeśli program Azure AD Connect nie synchronizuje domyślnego zestawu atrybutów i został dostosowany do korzystania z filtrowanego zestawu atrybutów. W przeciwnym razie $false.
* StagingMode: $false (domyślnie) — jeśli serwer programu Azure AD Connect NIE JEST w trybie przejściowym, wartość $true, jeśli serwer jest skonfigurowany na tryb przejściowy.

Po wyświetleniu monitu o uwierzytelnienie musisz użyć tego samego konta administratora globalnego (na przykład admin@domain.onmicrosoft.com), które było używane podczas konfigurowania programu Azure AD Connect.

## <a name="installing-the-azure-ad-connect-health-agent-for-ad-ds"></a>Instalowanie agenta programu Azure AD Connect Health dla usług AD DS
Aby rozpocząć instalowanie agenta, kliknij dwukrotnie pobrany plik exe. Na pierwszym ekranie kliknij przycisk Instaluj.

![Weryfikowanie programu Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install1.png)

Po zakończeniu instalacji kliknij przycisk Konfiguruj teraz.

![Weryfikowanie programu Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install2.png)

Zostanie uruchomiony wiersz polecenia, a następnie pewne polecenia programu PowerShell, które spowodują wykonanie polecenia Register-AzureADConnectHealthADDSAgent. Po wyświetleniu monitu zaloguj się do platformy Azure.

![Weryfikowanie programu Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install3.png)

Po zalogowaniu się działanie programu PowerShell będzie kontynuowane. Gdy program PowerShell zakończy pracę, możesz go zamknąć. Konfiguracja zostanie zakończona.

W tym momencie usługi powinny uruchomić się automatycznie, umożliwiając agentowi monitorowanie i zbieranie danych. Jeśli nie zostały spełnione wszystkie wymagania wstępne, które zostały opisane w poprzednich sekcjach, w oknie programu PowerShell będą wyświetlane ostrzeżenia. Przed zainstalowaniem agenta upewnij się, że zostały spełnione [wymagania](active-directory-aadconnect-health-agent-install.md#requirements). Poniższy zrzut ekranu przedstawia przykład tego rodzaju błędów.

![Weryfikowanie programu Azure AD Connect Health dla usług AD DS](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install4.png)

Aby sprawdzić, czy agent został zainstalowany, znajdź następujące usługi na kontrolerze domeny:

* Usługa szczegółowych informacji usług AD DS programu Azure AD Connect Health
* Usługa monitorowania usług AD DS programu Azure AD Connect Health

Jeśli konfiguracja została zakończona, te usługi powinny być uruchomione. W przeciwnym razie pozostaną one zatrzymane do czasu zakończenia konfiguracji.

![Weryfikowanie programu Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install5.png)


### <a name="agent-registration-using-powershell"></a>Rejestracja agenta przy użyciu programu PowerShell
Po zainstalowaniu agenta za pomocą odpowiedniego pliku setup.exe możesz przeprowadzić rejestrację agenta przy użyciu poniższych poleceń programu PowerShell w zależności od roli. Otwórz okno programu PowerShell i wykonaj odpowiednie polecenie:

```
    Register-AzureADConnectHealthADFSAgent
    Register-AzureADConnectHealthADDSAgent
    Register-AzureADConnectHealthSyncAgent

```

W tych poleceniach akceptowana jest wartość „Credential” jako parametr w celu ukończenia rejestracji w sposób nieinterakcyjny bądź na maszynie z systemem Server Core.
* Wartość Credential może być przechowywana w zmiennej programu PowerShell przekazywanej jako parametr.
* Możesz użyć dowolnej tożsamości usługi Azure AD, która ma dostęp do rejestracji agentów i dla której NIE WŁĄCZONO uwierzytelniania MFA.
* Domyślnie administratorzy globalni mają dostęp do przeprowadzenia rejestracji agenta. Na wykonanie tego kroku możesz również zezwolić innym, mniej uprzywilejowanym tożsamościom. Przeczytaj więcej na temat [kontroli dostępu na podstawie ról](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control).

```
    $cred = Get-Credential
    Register-AzureADConnectHealthADFSAgent -Credential $cred

```

## <a name="configure-azure-ad-connect-health-agents-to-use-http-proxy"></a>Konfigurowanie agentów programu Azure AD Connect Health na potrzeby korzystania z serwera proxy HTTP
Agentów programu Azure AD Connect Health możesz skonfigurować tak, aby współpracowali z serwerem proxy HTTP.

> [!NOTE]
> * Polecenie „Netsh WinHttp set ProxyServerAddress” nie jest obsługiwane, ponieważ do wysyłania żądań sieci web agent używa przestrzeni nazw System.Net zamiast usług HTTP systemu Microsoft Windows.
> * Skonfigurowany adres serwera proxy HTTP jest używany do przekazywania szyfrowanych komunikatów HTTPS.
> * Uwierzytelniane (przy użyciu metody HTTPBasic) serwery proxy nie są obsługiwane.
>
>

### <a name="change-health-agent-proxy-configuration"></a>Zmienianie konfiguracji serwera proxy agenta kondycji
Agenta programu Azure AD Connect Health możesz skonfigurować na potrzeby korzystania z serwera proxy HTTP za pomocą poniższych opcji.

> [!NOTE]
> Aby ustawienia serwera proxy zostały zaktualizowane, musisz uruchomić ponownie wszystkie usługi agenta programu Azure AD Connect Health. Uruchom następujące polecenie:<br>
> Restart-Service AdHealth*
>
>

#### <a name="import-existing-proxy-settings"></a>Importowanie istniejących ustawień serwera proxy
##### <a name="import-from-internet-explorer"></a>Importowanie z programu Internet Explorer
Ustawienia serwera HTTP programu Internet Explorer można zaimportować do użycia przez agentów programu Azure AD Connect Health. Na wszystkich serwerach z uruchomionym agentem programu Health wykonaj następujące polecenie programu PowerShell:

    Set-AzureAdConnectHealthProxySettings -ImportFromInternetSettings

##### <a name="import-from-winhttp"></a>Importowanie z usług WinHTTP
Ustawienia serwera proxy WinHTTP można zaimportować do użycia przez agentów programu Azure AD Connect Health. Na wszystkich serwerach z uruchomionym agentem programu Health wykonaj następujące polecenie programu PowerShell:

    Set-AzureAdConnectHealthProxySettings -ImportFromWinHttp

#### <a name="specify-proxy-addresses-manually"></a>Ręczne określanie adresów serwerów proxy
Serwer proxy możesz określić ręcznie na każdym serwerze, na którym jest uruchomiony agent kondycji, wykonując następujące polecenie programu PowerShell:

    Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress address:port

Przykład: *Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress mojserwerproxy: 443*

* Parametr „address” może być rozpoznawalną nazwą serwera w systemie DNS lub adresem IPv4.
* Parametr „port” można pominąć. W przypadku pominięcia jako domyślny zostanie wybrany port 443.

#### <a name="clear-existing-proxy-configuration"></a>Czyszczenie istniejącej konfiguracji serwera proxy
Istniejącą konfigurację serwera proxy możesz wyczyścić, uruchamiając następujące polecenie:

    Set-AzureAdConnectHealthProxySettings -NoProxy


### <a name="read-current-proxy-settings"></a>Odczytywanie bieżących ustawień serwera proxy
Możesz odczytać aktualnie skonfigurowane ustawienia serwera proxy, wykonując następujące polecenie:

    Get-AzureAdConnectHealthProxySettings


## <a name="test-connectivity-to-azure-ad-connect-health-service"></a>Testowanie łączności z usługą Azure AD Connect Health
Mogą wystąpić problemy powodujące utratę łączności agenta programu Azure AD Connect Health z usługą Azure AD Connect Health. Ich przyczyną mogą być problemy z siecią, problemy z uprawnieniami lub różne inne czynniki.

Jeśli agent nie może wysyłać danych do programu Azure AD Connect Health przez ponad 2 godziny, w portalu zostanie wyświetlony alert o treści „Dane usługi kondycji są nieaktualne”. Możesz sprawdzić, czy agent programu Azure AD Connect Health, którego dotyczy alert, jest w stanie przekazywać dane do usługi Azure AD Connect Health, wykonując następujące polecenie programu PowerShell:

    Test-AzureADConnectHealthConnectivity -Role ADFS

Parametr roli obecnie przyjmuje następujące wartości:

* ADFS
* Sync
* ADDS

Aby wyświetlić szczegółowe dzienniki, możesz użyć w poleceniu flagi -ShowResults. Skorzystaj z następującego przykładu:

    Test-AzureADConnectHealthConnectivity -Role Sync -ShowResult

> [!NOTE]
> Aby korzystać z narzędzia łączności, najpierw musisz zakończyć rejestrację agenta. Jeśli nie możesz zakończyć rejestracji agenta, upewnij się, że zostały spełnione wszystkie [wymagania](active-directory-aadconnect-health-agent-install.md#requirements) programu Azure AD Connect Health. Ten test łączności jest wykonywany domyślnie podczas rejestracji agenta.
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
