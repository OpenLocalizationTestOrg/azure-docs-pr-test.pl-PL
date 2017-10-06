---
title: 'Azure AD Connect: Automatyczne uaktualnianie | Dokumentacja firmy Microsoft'
description: W tym temacie opisano hello automatycznego uaktualniania funkcja wbudowana w synchronizacji Azure AD Connect.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b395e8f-fa3c-4e55-be54-392dd303c472
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 70d15eb3adf7758d8a43d278157daa504e059a98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-automatic-upgrade"></a>Azure AD Connect: automatyczne uaktualnianie
Ta funkcja została wprowadzona z kompilacją 1.1.105.0 (wydane luty 2016).

## <a name="overview"></a>Omówienie
Zapewnienie instalacji programu Azure AD Connect jest zawsze aktywna toodate jest wyjątkowo proste z hello **automatyczne uaktualnianie** funkcji. Ta funkcja jest włączona domyślnie w przypadku instalacji ekspresowej, a uaktualnienie narzędzia DirSync. Po wydaniu nowej wersji instalacji zostaje automatycznie uaktualnione.

Automatyczne uaktualnianie jest domyślnie włączona dla następujących hello:

* Express ustawienia instalacji i uaktualnienia narzędzia DirSync.
* Za pomocą programu SQL Express LocalDB, czyli co ustawień ekspresowych zawsze używać. Narzędzie DirSync z programu SQL Express również użyć LocalDB.
* Witaj konta AD jest hello domyślne MSOL_ konto utworzone przez ustawień ekspresowych oraz narzędzia DirSync.
* Masz mniej niż 100 000 obiektów w magazynie metaverse hello.

bieżący stan Hello automatycznego uaktualnienia można wyświetlić za pomocą polecenia cmdlet programu PowerShell hello `Get-ADSyncAutoUpgrade`. Ma hello następujące stany:

| Stan | Komentarz |
| --- | --- |
| Enabled (Włączony) |Włączono automatyczną aktualizację. |
| Zawieszone |Ustaw przez system hello tylko. Witaj systemu nie jest już kwalifikujących się tooreceive automatycznych uaktualnień. |
| Disabled (Wyłączony) |Automatyczne uaktualnianie jest wyłączona. |

Można przełączać się między **włączone** i **wyłączone** z `Set-ADSyncAutoUpgrade`. Tylko hello system należy ustawić stanu hello **zawieszone**.

Automatyczne uaktualnianie używa usługi Azure AD Connect Health hello uaktualnienia infrastruktury. Do automatycznego uaktualniania toowork, upewnij się, że adresy URL hello został otwarty na serwerze proxy dla **Azure AD Connect Health** zgodnie z opisem w [zakresów adresów IP i URL usługi Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

Jeśli hello **Menedżera usługi synchronizacji** interfejsu użytkownika jest uruchomiona na powitania serwera, a następnie hello uaktualnienia jest wstrzymane do czasu zamknięcia hello interfejsu użytkownika.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Jeśli instalacji Connect nie uaktualnia się sam zgodnie z oczekiwaniami, postępuj zgodnie toofind te kroki się, jakie może być nieprawidłowy.

Najpierw należy nie oczekiwać hello automatycznego uaktualniania toobe podjęto hello pierwszego dnia wydana nowa wersja. Jest zamierzone losowości przed próbą uaktualnienia, więc nie alarmed instalacji nie jest od razu uaktualnienia.

Jeśli uważasz, że nie jest element w prawo, najpierw uruchom `Get-ADSyncAutoUpgrade` tooensure automatyczne uaktualnianie jest włączona.

Następnie upewnij się, że adresy URL hello wymagane został otwarty w użyciu serwera proxy lub zapory. Aktualizacje automatyczne jest przy użyciu usługi Azure AD Connect Health, zgodnie z opisem w hello [omówienie](#overview). Jeśli używasz serwera proxy, upewnij się, kondycji został skonfigurowany toouse [serwera proxy](../connect-health/active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy). Także przetestować hello [łączności kondycji](../connect-health/active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service) tooAzure AD.

TooAzure łączności hello AD zweryfikowane jest toolook czas na powitania elementami EventLog. Uruchomienie podglądu zdarzeń hello i Znajdź hello **aplikacji** eventlog. Dodaj filtr dziennika zdarzeń dla źródła hello **Azure AD Connect uaktualnienia** i zakres identyfikatora zdarzenia hello **300 399**.  
![Filtr dziennika zdarzeń dla automatycznego uaktualniania](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogfilter.png)  

Możesz teraz przeglądać elementami EventLog hello skojarzony ze stanem hello do automatycznego uaktualnienia.  
![Filtr dziennika zdarzeń dla automatycznego uaktualniania](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogresult.png)  

Kod wyniku Hello ma prefiks przegląd stanu hello.

| Prefiks kod wyniku | Opis |
| --- | --- |
| Powodzenie |Pomyślnie uaktualniono Hello instalacji. |
| UpgradeAborted |Tymczasowy warunek zatrzymana hello uaktualnienia. Zostanie ona ponownie ponowione i hello oczekuje się, czy próba powiedzie się później. |
| UpgradeNotSupported |Hello system ma konfigurację, która blokuje hello system z uaktualniany automatycznie. Będzie ponawiane toosee hello stan jest zmieniany, ale hello oczekuje się, że hello system muszą zostać uaktualnione ręcznie. |

Oto lista znalezionej wiadomości powitania najczęściej. Nie wyświetla listy wszystkich, ale wiadomości powitania wynik powinien być Wyczyść z jaki problem hello jest.

| Komunikat o wyniku | Opis |
| --- | --- |
| **UpgradeAborted** | |
| UpgradeAbortedCouldNotSetUpgradeMarker |Nie można zapisać rejestru toohello. |
| UpgradeAbortedInsufficientDatabasePermissions |grupy wbudowanych administratorów Hello nie ma uprawnienia toohello w bazie danych. Ręcznie Uaktualnij toohello najnowszą wersję programu Azure AD Connect tooaddress ten problem. |
| UpgradeAbortedInsufficientDiskSpace |Uaktualnienie nie jest za mało toosupport miejsca na dysku. |
| UpgradeAbortedSecurityGroupsNotPresent |Nie można odnaleźć i rozwiązać wszystkie grupy zabezpieczeń używane przez aparat synchronizacji hello. |
| UpgradeAbortedServiceCanNotBeStarted |Witaj usługi NT **Microsoft Azure AD Sync** nie powiodło się toostart. |
| UpgradeAbortedServiceCanNotBeStopped |Witaj usługi NT **Microsoft Azure AD Sync** nie powiodło się toostop. |
| UpgradeAbortedServiceIsNotRunning |Witaj usługi NT **Microsoft Azure AD Sync** nie jest uruchomiona. |
| UpgradeAbortedSyncCycleDisabled |Witaj SyncCycle opcji hello [harmonogramu](active-directory-aadconnectsync-feature-scheduler.md) została wyłączona. |
| UpgradeAbortedSyncExeInUse |Witaj [interfejs użytkownika Menedżera usługi synchronizacji](active-directory-aadconnectsync-service-manager-ui.md) jest otwarty na powitania serwera. |
| UpgradeAbortedSyncOrConfigurationInProgress |Kreator instalacji Hello jest uruchomiony lub synchronizacji zostało zaplanowane poza hello harmonogramu. |
| **UpgradeNotSupported** | |
| UpgradeNotSupportedCustomizedSyncRules |Dodano własne reguły niestandardowe toohello konfiguracji. |
| UpgradeNotSupportedDeviceWritebackEnabled |Włączono hello [zapisu zwrotnego urządzeń](active-directory-aadconnect-feature-device-writeback.md) funkcji. |
| UpgradeNotSupportedGroupWritebackEnabled |Włączono hello [zapisu zwrotnego grup](active-directory-aadconnect-feature-preview.md#group-writeback) funkcji. |
| UpgradeNotSupportedInvalidPersistedState |Witaj, instalacja nie jest ustawień ekspresowych lub uaktualnienie narzędzia DirSync. |
| UpgradeNotSupportedMetaverseSizeExceeeded |Masz więcej niż 100 000 obiektów w magazynie metaverse hello. |
| UpgradeNotSupportedMultiForestSetup |Łączysz toomore niż jednym lesie. Instalacja ekspresowa łączy tylko tooone lasu. |
| UpgradeNotSupportedNonLocalDbInstall |Nie używasz bazy danych programu SQL Server Express LocalDB. |
| UpgradeNotSupportedNonMsolAccount |Witaj [konta łącznika AD](active-directory-aadconnect-accounts-permissions.md#active-directory-account) nie jest hello domyślnego konta MSOL_ już. |
| UpgradeNotSupportedStagingModeEnabled |Serwer Hello jest ustawiony toobe [Tryb przejściowy](active-directory-aadconnectsync-operations.md#staging-mode). |
| UpgradeNotSupportedUserWritebackEnabled |Włączono hello [zapisu zwrotnego użytkowników](active-directory-aadconnect-feature-preview.md#user-writeback) funkcji. |

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
