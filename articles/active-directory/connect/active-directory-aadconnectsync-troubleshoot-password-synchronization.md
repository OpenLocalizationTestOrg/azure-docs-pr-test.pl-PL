---
title: "Synchronizacja haseł aaaTroubleshoot z synchronizacji Azure AD Connect | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera informacje na temat problemów z synchronizacją hasła tootroubleshoot."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 390eafec792cb39251627c14cb754f8bb30035b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a>Rozwiązywanie problemów z synchronizacją hasła z synchronizacji Azure AD Connect
Ten temat zawiera kroki opisujące sposób tootroubleshoot problemy z synchronizacją haseł. Jeśli nie można zsynchronizować hasła, zgodnie z oczekiwaniami, można dla podzbioru użytkowników lub dla wszystkich użytkowników. Dla usługi Azure Active Directory (Azure AD) wdrożenia Uzyskuj dostęp do wersji 1.1.524.0 lub później, jest teraz diagnostycznych polecenia cmdlet można tootroubleshoot problemów z synchronizacją hasła:

* Jeśli masz problem, których hasła nie są zsynchronizowane, zapoznaj się z pomocą techniczną firmy toohello [hasła nie są zsynchronizowane: Rozwiązywanie problemów przy użyciu polecenia cmdlet diagnostycznych hello](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) sekcji.

* Jeśli masz problem z pojedyncze obiekty, zapoznaj się z pomocą techniczną firmy toohello [jeden obiekt nie synchronizuje haseł: Rozwiązywanie problemów przy użyciu polecenia cmdlet diagnostycznych hello](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) sekcji.

Dla wcześniejszych wersji programu Azure AD Connect wdrażania:

* Jeśli masz problem, których hasła nie są zsynchronizowane, zapoznaj się z pomocą techniczną firmy toohello [hasła nie są zsynchronizowane: Podręcznik rozwiązywania problemów z](#no-passwords-are-synchronized-manual-troubleshooting-steps) sekcji.

* Jeśli masz problem z pojedyncze obiekty, zapoznaj się z pomocą techniczną firmy toohello [jeden obiekt nie synchronizuje haseł: Podręcznik rozwiązywania problemów z](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) sekcji.

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>Hasła nie są zsynchronizowane: Rozwiązywanie problemów przy użyciu polecenia cmdlet diagnostycznych hello
Można użyć hello `Invoke-ADSyncDiagnostics` toofigure polecenia cmdlet się, dlaczego hasła nie są zsynchronizowane.

> [!NOTE]
> Witaj `Invoke-ADSyncDiagnostics` polecenia cmdlet jest dostępna tylko dla wersji Azure AD Connect 1.1.524.0 lub nowszej.

### <a name="run-hello-diagnostics-cmdlet"></a>Uruchom polecenie cmdlet diagnostyki hello
tootroubleshoot problemy, których hasła nie są zsynchronizowane:

1. Otwórz sesję programu Windows PowerShell na serwerze programu Azure AD Connect z hello **Uruchom jako Administrator** opcji.

2. Uruchom `Set-ExecutionPolicy RemoteSigned` lub `Set-ExecutionPolicy Unrestricted`.

3. Uruchom polecenie `Import-Module ADSyncDiagnostics`.

4. Uruchom polecenie `Invoke-ADSyncDiagnostics -PasswordSync`.

### <a name="understand-hello-results-of-hello-cmdlet"></a>Zrozumienie hello wyniki polecenia cmdlet hello
polecenia cmdlet diagnostycznych Hello wykonuje powitania po kontroli:

* Sprawdza poprawność tego hello funkcji synchronizacji haseł jest włączona dla Twojej dzierżawy usługi Azure AD.

* Sprawdza poprawność tego hello Azure AD Connect, serwer nie jest w trybie przejściowym.

* Dla każdego istniejącego lokalnego łącznika usługi Active Directory, (co odpowiada tooan istniejącego lasu usługi Active Directory):

   * Sprawdza poprawność tego hello jest włączona funkcja synchronizacji hasła.
   
   * Wyszukuje zdarzeń pulsu synchronizacji haseł w hello dzienniki zdarzeń aplikacji systemu Windows.

   * Dla każdej domeny usługi Active Directory, w obszarze łącznika usługi Active Directory lokalne powitania:

      * Sprawdza poprawność tego hello domena jest osiągalna z hello Azure AD Connect serwera.

      * Sprawdza, czy konta usług domenowych w usłudze Active Directory (AD DS) hello używane przez łącznik usługi Active Directory lokalne powitania ma hello prawidłową nazwę użytkownika, hasło i uprawnienia wymagane do synchronizacji haseł.

powitania po diagram ilustruje hello wyniki polecenia cmdlet hello Topologia jednej domenie lokalnej usługi Active Directory:

![Dane wyjściowe diagnostyki dla synchronizacji haseł](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

Witaj pozostałej części tej sekcji opisano określone wyniki, które są zwracane przez polecenie cmdlet hello i odpowiednie problemy.

#### <a name="password-synchronization-feature-isnt-enabled"></a>Funkcja synchronizacji hasła nie jest włączona.
Jeśli nie włączono synchronizacji haseł za pomocą kreatora Połącz hello Azure AD, jest zwracany hello następujący błąd:

![Synchronizacja haseł nie jest włączona.](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a>Serwer systemu Azure AD Connect jest w trybie przejściowym
Jeśli hello Azure AD Connect serwer działa w trybie przejściowym, synchronizacja haseł jest tymczasowo wyłączona i hello następujące zostanie zwrócony błąd:

![Serwer systemu Azure AD Connect jest w trybie przejściowym](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a>Brak zdarzeń pulsu synchronizacji haseł
Każdy łącznik usługi Active Directory lokalnego ma własną kanału synchronizacji haseł. Po nawiązaniu kanału synchronizacji haseł hello i nie ma żadnych toobe zmiany hasła zsynchronizowane, co 30 minut w dzienniku zdarzeń aplikacji systemu Windows hello zostanie wygenerowane zdarzenie pulsu (identyfikator EventId 654). Przez każdy łącznik usługi Active Directory lokalne powitania polecenie cmdlet wyszukuje, poszukaj pokrewnych zdarzeń pulsu w hello ostatnich trzech godzin. Jeśli żadne zdarzenie pulsu zostanie znaleziony, hello następujące zostanie zwrócony błąd:

![Nie pulsu synchronizacji haseł Ci zdarzeń](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a>Usługi AD DS konto nie ma odpowiednich uprawnień
Jeśli konto hello usług AD DS, które jest używane przez hello lokalnego skrótów haseł toosynchronize łącznika usługi Active Directory nie ma odpowiednich uprawnień hello hello następujące zostanie zwrócony błąd:

![Nieprawidłowe poświadczenia](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a>Nieprawidłowa nazwa użytkownika konta usług AD DS lub hasło
Jeśli hello konta usług AD DS używany przez hello skrótów haseł toosynchronize lokalnej usługi Active Directory łącznika ma nieprawidłową nazwą użytkownika lub hasło, hello następujące zostanie zwrócony błąd:

![Nieprawidłowe poświadczenia](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>Jeden obiekt nie synchronizuje haseł: Rozwiązywanie problemów przy użyciu polecenia cmdlet diagnostycznych hello
Można użyć hello `Invoke-ADSyncDiagnostics` toodetermine polecenia cmdlet, dlaczego jeden obiekt nie synchronizuje haseł.

> [!NOTE]
> Witaj `Invoke-ADSyncDiagnostics` polecenia cmdlet jest dostępna tylko dla wersji Azure AD Connect 1.1.524.0 lub nowszej.

### <a name="run-hello-diagnostics-cmdlet"></a>Uruchom polecenie cmdlet diagnostyki hello
tootroubleshoot problemy, których hasła nie są zsynchronizowane:

1. Otwórz sesję programu Windows PowerShell na serwerze programu Azure AD Connect z hello **Uruchom jako Administrator** opcji.

2. Uruchom `Set-ExecutionPolicy RemoteSigned` lub `Set-ExecutionPolicy Unrestricted`.

3. Uruchom polecenie `Import-Module ADSyncDiagnostics`.

4. Uruchom następujące polecenia cmdlet hello:
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   Na przykład:
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a>Zrozumienie hello wyniki polecenia cmdlet hello
polecenia cmdlet diagnostycznych Hello wykonuje powitania po kontroli:

* Sprawdza stan hello hello obiektu usługi Active Directory w przestrzeni łącznika usługi Active Directory hello Metaverse i Azure AD przestrzeni łącznika.

* Sprawdza, czy są reguły synchronizacji z synchronizacją haseł włączone i stosowane toohello obiektu usługi Active Directory.

* Próbuje tooretrieve i wyświetlania wyników hello hello ostatniej próby toosynchronize hello hasła dla obiekt hello.

powitania po diagram ilustruje hello wyniki polecenia cmdlet hello podczas rozwiązywania problemów z synchronizacji haseł dla pojedynczego obiektu:

![Dane wyjściowe diagnostyki dla synchronizacji haseł — pojedynczy obiekt](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

Witaj pozostałej części tej sekcji opisano określonych wyników zwróconych przez polecenie cmdlet hello i odpowiednie problemy.

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a>Hello obiektu usługi Active Directory nie jest eksportowany tooAzure AD
Synchronizacja haseł dla tego konta usługi Active Directory lokalnymi nie powiedzie się, ponieważ nie ma odpowiedniego obiektu w hello dzierżawy usługi Azure AD. Zwrócono Hello następujący błąd:

![Brak obiektu usługi Active Directory systemu Azure](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a>Użytkownik ma hasło tymczasowe
Azure AD Connect nie obsługuje obecnie synchronizowanie tymczasowego hasła z usługą Azure AD. Hasło jest uznawany za toobe tymczasowego Jeśli hello **zmienić hasło przy następnym logowaniu** opcja jest ustawiona na powitania lokalnej usługi Active Directory użytkownika. Zwrócono Hello następujący błąd:

![Hasło tymczasowe nie są eksportowane.](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a>Wyniki ostatniej próby toosynchronize hasła nie są dostępne
Domyślnie program Azure AD Connect przechowuje wyniki hello prób synchronizacji haseł na siedem dni. Jeśli nie są dostępne dla obiekt usługi Active Directory hello wybrane wyniki, zwracany jest hello następujące ostrzeżenie:

![Dane wyjściowe diagnostyki dla pojedynczego obiektu — nie historii synchronizacji haseł](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a>Hasła nie są zsynchronizowane: ręczne kroki rozwiązywania problemów
Wykonaj te kroki toodetermine, dlaczego hasła nie są zsynchronizowane:

1. Jest serwerem Connect hello w [Tryb przejściowy](active-directory-aadconnectsync-operations.md#staging-mode)? Serwer w trybie przejściowym nie synchronizować hasła.

2. Uruchom skrypt hello w hello [Pobierz stan hello ustawień synchronizacji hasła](#get-the-status-of-password-sync-settings) sekcji. Udostępnia przegląd konfiguracji synchronizacji haseł hello.  

    ![Dane wyjściowe skryptu programu PowerShell z ustawień synchronizacji haseł](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. Nie włączono funkcji hello w usłudze Azure AD lub stan kanału synchronizacji hello nie jest włączona, uruchom Kreatora instalacji Connect hello. Wybierz **Dostosuj opcje synchronizacji**i usuń zaznaczenie pozycji synchronizacji haseł. Ta zmiana tymczasowo wyłącza funkcję hello. Następnie uruchom ponownie kreatora hello i ponowne włączenie synchronizacji haseł. Uruchom skrypt hello ponownie tooverify, który hello konfiguracji są poprawne.

4. Poszukaj w dzienniku zdarzeń hello błędów. Wyszukaj hello następujące zdarzenia, które wskazują problem:
    * Źródła: Identyfikator "Synchronizacji katalogów": 0, 611, 652, 655, jeśli te zdarzenia są widoczne masz problem z połączeniem. Hello komunikatu dziennika zdarzeń zawiera informacje lasu, gdzie występuje problem. Aby uzyskać więcej informacji, zobacz [problem z łącznością](#connectivity problem).

5. Jeśli widzisz Brak pulsu lub pracuje zaczynającego, uruchom [wyzwolenia pełnej synchronizacji haseł wszystkich](#trigger-a-full-sync-of-all-passwords). Uruchom skrypt hello tylko raz.

6. Zobacz hello [Rozwiązywanie problemów z jednego obiektu, który nie jest synchronizowanie haseł](#one-object-is-not-synchronizing-passwords) sekcji.

### <a name="connectivity-problems"></a>Problemy z łącznością

Czy masz połączenie z usługą Azure AD?

Konto hello wymaganych wartości skrótów haseł hello tooread uprawnienia we wszystkich domenach? Jeśli zainstalowano Połącz przy użyciu ustawień ekspresowych hello uprawnień powinna już być poprawne. 

Jeśli używasz niestandardowej instalacji, należy ręcznie ustawić uprawnienia hello hello następujący:
    
1. toofind hello konto używane przez łącznik usługi Active Directory hello, start **Menedżera usługi synchronizacji**. 
 
2. Przejdź za**łączniki**, a następnie wyszukaj lasu usługi Active Directory lokalne powitania rozwiązywania problemów. 
 
3. Wybierz łącznik hello, a następnie kliknij przycisk **właściwości**. 
 
4. Przejdź za**Connect lesie katalogu tooActive**.  
    
    ![Konto używane przez łącznik usługi Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    Należy pamiętać, hello nazwę użytkownika i domenę hello, w której znajduje się konto hello.
    
5. Uruchom **użytkownicy usługi Active Directory i komputery**, a następnie sprawdź, czy konto hello znalezionych w wcześniej ma uprawnienia wykonaj hello ustawione w głównym hello wszystkich domen w lesie:
    * Replikować zmiany katalogu
    * Replikowanie katalogu zmienia wszystkie

6. Czy hello kontrolerów domeny jest dostępny przy użyciu programu Azure AD Connect? Jeśli hello Połącz serwer nie może połączyć tooall kontrolerów domeny, należy skonfigurować **tylko Użyj preferowanego kontrolera domeny**.  
    
    ![Kontroler domeny jest używany przez łącznik usługi Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. Wróć za**Menedżera usługi synchronizacji** i **Konfigurowanie partycji katalogu**. 
 
8. Wybierz domenę w **Wybieranie partycji katalogu**, wybierz pozycję hello **korzystają z kontrolerów domeny preferowanych** pole wyboru, a następnie kliknij przycisk **Konfiguruj**. 

9. Na liście hello wprowadź hello kontrolerów domeny, które Connect należy używać do synchronizacji haseł. Witaj, importowania i eksportowania również jest używana w tej samej listy. Wykonaj te kroki dla wszystkich domen.

10. Jeśli skrypt hello pokazuje, że jest brak pulsu, uruchom skrypt hello w [wyzwolenia pełnej synchronizacji haseł wszystkich](#trigger-a-full-sync-of-all-passwords).

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a>Jeden obiekt nie synchronizuje haseł: ręczne kroki rozwiązywania problemów
Umożliwia łatwe rozwiązywanie problemów z synchronizacją hasła, przeglądając hello stanu obiektu.

1. W **użytkownicy usługi Active Directory i komputery**, wyszukaj hello użytkownika, a następnie sprawdź tego hello **użytkownik musi zmienić hasło przy następnym logowaniu** pole wyboru jest wyczyszczone.  

    ![Active Directory produktywności hasła.](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    Jeśli zaznaczono pole wyboru hello, poproś hello toosign użytkownika w i Zmień hasło hello. Tymczasowe hasła nie są zsynchronizowane z usługą Azure AD.

2. Jeśli hasło hello wygląda poprawnie w usłudze Active Directory, wykonaj użytkownika hello hello aparatu synchronizacji. Przez następujący użytkownik hello z lokalnej usługi Active Directory tooAzure AD widać, czy w obiekcie hello jest opisem błędu.

    a. Uruchom hello [Menedżera usługi synchronizacji](active-directory-aadconnectsync-service-manager-ui.md).

    b. Kliknij przycisk **łączniki**.

    c. Wybierz hello **łącznika usługi Active Directory** którym znajduje się hello użytkownika.

    d. Wybierz **wyszukiwania przestrzeni łącznika**.

    e. W hello **zakres** wybierz opcję **nazwa Wyróżniająca lub zakotwiczenia**, a następnie wprowadź hello Pełna nazwa Wyróżniająca użytkownika hello rozwiązywania problemów.

    ![Wyszukaj użytkownika w przestrzeni łącznika o nazwie Wyróżniającej](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    f. Znajdź użytkownika hello szukasz, a następnie kliknij przycisk **właściwości** toosee hello wszystkie atrybuty. Sprawdź, czy hello użytkownika nie jest w wyniku wyszukiwania hello, Twoje [reguły filtrowania](active-directory-aadconnectsync-configure-filtering.md) i upewnij się, że uruchamiasz [Zastosuj i Sprawdź zmiany](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) dla tooappear użytkownika hello w Connect.

    g. Kliknij zeszłym tygodniu toosee hello hasła synchronizacji Szczegóły obiektu hello hello **dziennika**.  

    ![Szczegóły dziennika obiektu](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    Jeśli dziennik obiektu hello jest pusta, Azure AD Connect została skrót hasła hello tooread z usługi Active Directory. Kontynuuj rozwiązywanie problemów z [błędów połączenia](#connectivity-errors). Jeśli widzisz innych wartości niż **Powodzenie**, można znaleźć tabeli toohello [Dziennik synchronizacji haseł](#password-sync-log).

    h. Wybierz hello **elementy powiązane** karcie i upewnij się, reguły synchronizacji co najmniej jeden w hello **PasswordSync** kolumna jest **True**. W konfiguracji domyślnej hello jest hello Nazwa reguły synchronizacji hello **w z usługi AD - AccountEnabled użytkownika**.  

    ![Elementy powiązane informacje o użytkowniku](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    i. Kliknij przycisk **właściwości obiektu Metaverse** toodisplay listę atrybutów użytkowników.  

    ![Informacje magazynie metaverse](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    Sprawdź, czy jest nie **cloudFiltered** atrybutu. Upewnij się, że atrybuty domeny hello (domainFQDN i domainNetBios) jest hello oczekiwanych wartości.

    j. Kliknij przycisk hello **łączniki** kartę. Upewnij się, że widoczny tooboth łączniki lokalnej usługi Active Directory i Azure AD.

    ![Informacje magazynie metaverse](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    k. Wybierz hello wiersza, który reprezentuje usługi Azure AD, kliknij przycisk **właściwości**, a następnie kliknij przycisk hello **elementy powiązane** kartę hello łącznika miejsca obiektu powinien mieć Reguła ruchu wychodzącego w hello **PasswordSync** zbyt zestawu kolumn**True**. W konfiguracji domyślnej hello jest hello Nazwa reguły synchronizacji hello **się tooAAD — użytkownik przyłączyć**.  

    ![Okno dialogowe właściwości obiektu obszaru łącznika](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a>Dziennik synchronizacji haseł
Witaj w kolumnie Stan może mieć hello następujące wartości:

| Stan | Opis |
| --- | --- |
| Powodzenie |Hasło zostało pomyślnie zsynchronizowane. |
| FilteredByTarget |Hasło jest ustawiane za**użytkownik musi zmienić hasło przy następnym logowaniu**. Hasło nie zostały zsynchronizowane. |
| NoTargetConnection |Brak obiektu hello metaverse lub przestrzeni łącznika hello Azure AD. |
| SourceConnectorNotPresent |Nie znaleziono w przestrzeni łącznika usługi Active Directory lokalne powitania obiektu. |
| TargetNotExportedToDirectory |Obiekt Hello w hello przestrzeni łącznika usługi Azure AD nie zostały wyeksportowane. |
| MigratedCheckDetailsForMoreInfo |Wpis dziennika został utworzony przed kompilacji 1.0.9125.0 i jest wyświetlany w stanie starszej wersji. |
| Błąd |Usługa zwróciła nieznany błąd. |
| Nieznany |Wystąpił błąd podczas próby tooprocess partii skrótów haseł.  |
| MissingAttribute |Określone atrybuty (na przykład protokołu Kerberos wyznaczania wartości skrótu) wymagane przez usługi domenowe Azure AD nie są dostępne. |
| RetryRequestedByTarget |Określone atrybuty (na przykład protokołu Kerberos wyznaczania wartości skrótu) wymagane przez usługi domenowe Azure AD nie były wcześniej dostępne. Następuje próba tooresynchronize hello skrót hasła użytkownika. |

## <a name="scripts-toohelp-troubleshooting"></a>Rozwiązywanie problemów z toohelp skryptów

### <a name="get-hello-status-of-password-sync-settings"></a>Pobierz stan hello ustawień synchronizacji haseł
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update hello script toouse hello appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a>Wyzwalacz pełnej synchronizacji haseł wszystkich
> [!NOTE]
> Ten skrypt należy uruchomić tylko raz. Jeśli potrzebujesz toorun on więcej niż raz, czegoś innego jest hello problem. tootroubleshoot hello problem, skontaktuj się z pomocą techniczną firmy Microsoft.

Możesz wyzwolić pełną synchronizację wszystkie hasła przy użyciu hello następującego skryptu:

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a>Następne kroki
* [Implementowanie synchronizacji haseł z synchronizacji Azure AD Connect](active-directory-aadconnectsync-implement-password-synchronization.md)
* [Azure AD Connect Sync: Dostosowywanie opcji synchronizacji](active-directory-aadconnectsync-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
