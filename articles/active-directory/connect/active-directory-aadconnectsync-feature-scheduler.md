---
title: 'Synchronizacja programu Azure AD Connect: harmonogram | Dokumentacja firmy Microsoft'
description: W tym temacie opisano hello funkcji wbudowanych harmonogram synchronizacji Azure AD Connect.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b1a598f-89c0-4244-9b20-f4aaad5233cf
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: c587039cc68d305862a07beff364894b6f74cd2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-scheduler"></a>Synchronizacja programu Azure AD Connect: harmonogramu
W tym temacie opisano hello wbudowanych harmonogramu synchronizacji Azure AD Connect () Aparat synchronizacji).

Ta funkcja została wprowadzona z kompilacją 1.1.105.0 (wydane luty 2016).

## <a name="overview"></a>Omówienie
Synchronizacja programu Azure AD Connect zsynchronizować zmiany zachodzące w katalogu lokalnym za pomocą harmonogramu. Istnieją dwa procesy harmonogramu dla synchronizacji haseł i drugi dla obiekt/atrybutu zadań synchronizacji i konserwacji. W tym temacie omówiono hello później.

We wcześniejszych wersjach hello harmonogramu dla obiektów i atrybutów zostało toohello zewnętrznych aparatu synchronizacji. Go użyć harmonogramu zadań systemu Windows lub osobnych Windows tootrigger hello proces synchronizacji usługi. Harmonogram Hello jest z hello 1.1 aparatu synchronizacji wbudowanych toohello wersje i umożliwienia pewne dostosowania. Hello nowe częstotliwość synchronizacji domyślny to 30 minut.

Harmonogram Hello jest odpowiedzialny za dwa zadania:

* **Cykl synchronizacji**. tooimport proces Hello, synchronizacji i zmian eksportu.
* **Zadania konserwacji**. Odnów klucze i certyfikaty służące do resetowania hasła i usługi rejestracji urządzeń (DRS). Przeczyszczać stare wpisy w dzienniku operacji hello.

Harmonogram Hello, sama zawsze jest uruchomiony, ale może być skonfigurowany tooonly uruchomienia co najmniej żadna z tych zadań. Na przykład należy toohave własnego procesu cyklu synchronizacji można wyłączyć tego zadania w harmonogramie hello, ale hello nadal wykonywania zadań konserwacji.

## <a name="scheduler-configuration"></a>Konfiguracja harmonogramu
toosee bieżących ustawień konfiguracji Przejdź tooPowerShell i uruchom `Get-ADSyncScheduler`. Przedstawia on podobny do tego obrazu:

![GetSyncScheduler](./media/active-directory-aadconnectsync-feature-scheduler/getsynccyclesettings2016.png)

Jeśli widzisz **polecenia synchronizacji hello lub polecenie cmdlet nie jest dostępna** po uruchomieniu tego polecenia cmdlet, następnie hello modułu programu PowerShell nie jest załadowany. Ten problem może się zdarzyć, jeśli uruchomisz Azure AD Connect na kontrolerze domeny lub na serwerze z wyższego poziomu ograniczeń programu PowerShell niż hello domyślnych ustawień. Jeśli zostanie wyświetlony ten błąd, uruchom `Import-Module ADSync` toomake hello polecenia cmdlet dostępne.

* **AllowedSyncCycleInterval**. Witaj najkrótszy odstęp czasu między cykle synchronizacji dozwolone przez usługę Azure AD. Nie można zsynchronizować częściej niż to ustawienie i nadal obsługiwane.
* **CurrentlyEffectiveSyncCycleInterval**. Witaj harmonogram obecnie efektu. Ma takie same wartości jak CustomizedSyncInterval hello (Jeśli ustawiona) Jeśli nie jest krótszy niż AllowedSyncInterval. Jeśli używasz kompilacji przed 1.1.281 i zmienić CustomizedSyncCycleInterval, to zmiany zostaną uwzględnione po następnym cyklu synchronizacji. Z kompilacji 1.1.281 zmiany hello aktywne natychmiast.
* **CustomizedSyncCycleInterval**. Jeśli chcesz toorun harmonogramu hello częstotliwością żadnych innych niż domyślne hello 30 minut, następnie dla tego ustawienia. Na rysunku powyżej hello hello harmonogram został ustawiony toorun co godzinę zamiast tego. Jeśli ustawisz wartość tooa ustawienie niższa niż AllowedSyncInterval, drugie hello jest używany.
* **NextSyncCyclePolicyType**. Delta lub początkowego. Określa, czy hello kolejnego uruchomienia należy tylko proces zmiany różnicowe, lub jeśli hello następnym uruchomieniu, należy wykonać pełny importowania i synchronizacji. ostatnie Hello będzie również ponownie przetworzyć żadnych reguł nowe lub zostały zmienione.
* **NextSyncCycleStartTimeInUTC**. Następnym uruchomieniu harmonogramu hello hello następnego cyklu synchronizacji.
* **PurgeRunHistoryInterval**. Witaj operację czas, który powinny być przechowywane dzienniki. Te dzienniki mogą być przeglądane na Menedżera usługi synchronizacji hello. Witaj domyślny jest tookeep te dzienniki 7 dni.
* **SyncCycleEnabled**. Wskazuje, czy harmonogramu hello działa hello importu, synchronizacji i procesy eksportu w ramach jego operacji.
* **MaintenanceEnabled**. Wskazuje, czy proces konserwacji hello jest włączona. Aktualizuje kluczy certyfikatów hello i powoduje usunięcie hello dziennika operacji.
* **StagingModeEnabled**. Pokazuje Jeśli [Tryb przejściowy](active-directory-aadconnectsync-operations.md#staging-mode) jest włączona. Jeśli to ustawienie jest włączone, następnie go pomija eksportuje hello uruchamiania, ale nadal uruchamiać importowania i synchronizacji.
* **SchedulerSuspended**. Ustawić Connect podczas uaktualniania tootemporarily bloku hello harmonogramu uruchamiania.

Można zmienić niektóre z tych ustawień z `Set-ADSyncScheduler`. można zmodyfikować Hello następujące parametry:

* CustomizedSyncCycleInterval
* NextSyncCyclePolicyType
* PurgeRunHistoryInterval
* SyncCycleEnabled
* MaintenanceEnabled

W starszych wersjach programu Azure AD Connect **isStagingModeEnabled** luk w ADSyncScheduler zestawu. Jest **nieobsługiwany** tooset tej właściwości. Witaj właściwości **SchedulerSuspended** powinien zostać zmodyfikowany tylko przez połączenie. Jest **nieobsługiwany** tooset to przy użyciu programu PowerShell bezpośrednio.

Konfiguracja harmonogramu Hello jest przechowywana w usłudze Azure AD. Jeśli masz serwer tymczasowej zmiany na serwerze podstawowym hello również ma wpływ na powitania serwera (z wyjątkiem IsStagingModeEnabled) na potrzeby przemieszczania.

### <a name="customizedsynccycleinterval"></a>CustomizedSyncCycleInterval
Składnia:`Set-ADSyncScheduler -CustomizedSyncCycleInterval d.HH:mm:ss`  
d — dni, HH - godziny, mm — minuty, ss — sekundy

Przykład:`Set-ADSyncScheduler -CustomizedSyncCycleInterval 03:00:00`  
Zmiany hello toorun harmonogramu co 3 godziny.

Przykład:`Set-ADSyncScheduler -CustomizedSyncCycleInterval 1.0:0:0`  
Zmiany zmianę toorun harmonogramu hello codziennie.

### <a name="disable-hello-scheduler"></a>Wyłączanie harmonogramu hello  
Jeśli potrzebujesz toomake zmian konfiguracji, ma toodisable hello harmonogramu. Na przykład, gdy użytkownik [skonfigurować filtrowanie](active-directory-aadconnectsync-configure-filtering.md) lub [zmiany reguły toosynchronization](active-directory-aadconnectsync-change-the-configuration.md).

Harmonogram hello toodisable, uruchom `Set-ADSyncScheduler -SyncCycleEnabled $false`.

![Wyłączanie harmonogramu hello](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)

Po dokonaniu zmiany, nie zapomnij harmonogramu hello tooenable ponownie, podając `Set-ADSyncScheduler -SyncCycleEnabled $true`.

## <a name="start-hello-scheduler"></a>Uruchamianie harmonogramu hello
Harmonogram Hello jest domyślnie uruchamiane co 30 minut. W niektórych przypadkach może być toorun cykl synchronizacji Between hello zaplanowane cykle lub należy toorun innego typu.

**Cykl synchronizacji różnicowej**  
Cykl synchronizacji różnicowej obejmuje hello następujące kroki:

* Import zmian dla wszystkich łączników
* Synchronizacja różnicowa dla wszystkich łączników
* Eksportowanie na wszystkich łączników

Jest to możliwe, że masz pilnych zmiany, która musi być synchronizowany natychmiast, dlatego należy toomanually uruchomienie cyklu. Jeśli potrzebujesz toomanually Uruchom cykl, następnie z programu PowerShell, uruchom `Start-ADSyncSyncCycle -PolicyType Delta`.

**Cykl pełnej synchronizacji**  
Jeden z hello następujące zmiany konfiguracji zostały wprowadzone, konieczne będzie toorun cyklu pełnej synchronizacji () Początkowy):

* Dodano więcej obiektów i atrybutów toobe zaimportowane z katalogu źródłowego
* Wprowadzone zmiany toohello reguły synchronizacji
* Zmienione [filtrowania](active-directory-aadconnectsync-configure-filtering.md) tak szereg różnych obiektów, należy włączyć

Jeśli wprowadzono jedną z tych zmian należy toorun cykl pełnej synchronizacji, więc aparat synchronizacji hello hello możliwości tooreconsolidate hello — obszary łączników. Cykl Pełna synchronizacja obejmuje hello następujące kroki:

* Pełny Import dla wszystkich łączników
* Pełna synchronizacja w wszystkich łączników
* Eksportowanie na wszystkich łączników

Uruchom tooinitiate cyklu pełnej synchronizacji `Start-ADSyncSyncCycle -PolicyType Initial` w wierszu programu PowerShell. To polecenie uruchamia cyklu pełnej synchronizacji.

## <a name="stop-hello-scheduler"></a>Zatrzymaj hello harmonogramu
Jeśli harmonogram hello jest aktualnie uruchomione cykl synchronizacji, może być konieczne toostop go. Na przykład jeśli możesz uruchomić Kreatora instalacji hello i ten błąd:

![SyncCycleRunningError](./media/active-directory-aadconnectsync-feature-scheduler/synccyclerunningerror.png)

Podczas cyklu synchronizacji jest uruchomiona, nie można wprowadzić zmian w konfiguracji. Można czekanie, aż harmonogramu hello zakończył proces hello, ale Zatrzymaj ją również, dzięki czemu można zmieniać zmiany natychmiast. Zatrzymywanie hello bieżącego cyklu nie jest szkodliwe i oczekujących zmian są przetwarzane kolejnego uruchomienia.

1. Rozpocząć od informacją o bieżącym hello toostop harmonogramu cyklu za pomocą polecenia cmdlet programu PowerShell hello `Stop-ADSyncSyncCycle`.
2. Jeśli używasz kompilacji przed 1.1.281, a następnie zatrzymywanie harmonogramu hello nie zatrzymuje hello bieżącego łącznika z jego bieżącego zadania. tooforce hello toostop łącznika, podjąć hello następujące akcje: ![StopAConnector](./media/active-directory-aadconnectsync-feature-scheduler/stopaconnector.png)
   * Uruchom **usługi synchronizacji** z hello start menu. Przejdź za**łączniki**, zaznacz hello łącznika ze stanem hello **systemem**i wybierz **zatrzymać** z hello akcje.

Hello harmonogram jest nadal aktywna i uruchamia ponownie w następnym możliwości.

## <a name="custom-scheduler"></a>Harmonogram niestandardowy
Witaj poleceń cmdlet w tej sekcji są dostępne tylko w kompilacji [1.1.130.0](active-directory-aadconnect-version-history.md#111300) i nowszych.

Harmonogram wbudowanych hello nie spełnia wymagań, można zaplanować łączniki hello przy użyciu programu PowerShell.

### <a name="invoke-adsyncrunprofile"></a>Wywołanie ADSyncRunProfile
Można uruchomić profilu dla łącznika w ten sposób:

```
Invoke-ADSyncRunProfile -ConnectorName "name of connector" -RunProfileName "name of profile"
```

Witaj toouse nazwy dla [nazw łączników](active-directory-aadconnectsync-service-manager-ui-connectors.md) i [nazwy profilu Uruchom](active-directory-aadconnectsync-service-manager-ui-connectors.md#configure-run-profiles) można znaleźć w hello [interfejsu użytkownika Menedżera usługi synchronizacji](active-directory-aadconnectsync-service-manager-ui.md).

![Wywołanie profilu uruchamiania](./media/active-directory-aadconnectsync-feature-scheduler/invokerunprofile.png)  

Witaj `Invoke-ADSyncRunProfile` polecenia cmdlet jest synchroniczne, czyli nie zwraca sterowania aż do zakończenia operacji hello hello łącznika, pomyślnie lub z powodu błędu.

Podczas planowania łączniki hello zaleca tooschedule je hello w następującej kolejności:

1. (Full/Delta) Importuj z katalogów lokalnych, takich jak usługi Active Directory
2. (Full/Delta) Importuj z usługi Azure AD
3. (Full/Delta) Synchronizacja z katalogów lokalnych, takich jak usługi Active Directory
4. (Full/Delta) Synchronizacja z usługą Azure AD
5. Eksportuj tooAzure AD
6. Eksportowanie lokalnych tooon katalogi, takich jak usługi Active Directory

Porządek ten jest działania łączników hello hello wbudowanych harmonogramu.

### <a name="get-adsyncconnectorrunstatus"></a>Get-ADSyncConnectorRunStatus
Można również monitorować toosee aparatu synchronizacji hello, jeżeli jest zajęty lub bezczynności. To polecenie cmdlet zwraca żadnego wyniku, jeśli aparat synchronizacji hello jest w stanie bezczynności i łącznika nie jest uruchomiona. Jeśli łącznik jest uruchomiona, zwraca nazwę hello hello łącznika.

```
Get-ADSyncConnectorRunStatus
```

![Stan uruchomienia łącznika](./media/active-directory-aadconnectsync-feature-scheduler/getconnectorrunstatus.png)  
Witaj ilustracji powyżej hello pierwszy wiersz jest ze stanu, w którym hello aparat synchronizacji jest w stanie bezczynności. drugi wiersz Hello z gdy hello łącznika usługi Azure AD jest uruchomiona.

## <a name="scheduler-and-installation-wizard"></a>Kreator harmonogramu i instalacji
Po uruchomieniu Kreatora instalacji hello harmonogramu hello tymczasowo jest wstrzymane. To zachowanie jest, ponieważ zakłada się zmian konfiguracji i nie można zastosować te ustawienia, jeśli aparat synchronizacji hello jest aktywnie wykonywane. Z tego powodu nie może pozostać Kreatora instalacji hello Otwórz ponieważ przestaje hello aparatu synchronizacji z wykonywania żadnych czynności synchronizacji.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o hello [synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md) konfiguracji.

Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
