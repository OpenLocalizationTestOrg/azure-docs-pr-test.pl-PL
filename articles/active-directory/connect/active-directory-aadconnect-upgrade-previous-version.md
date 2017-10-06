---
title: 'Azure AD Connect: Uaktualnianie z poprzedniej wersji | Dokumentacja firmy Microsoft'
description: "W tym artykule wyjaśniono hello różnych metod tooupgrade toohello najnowszej wersji programu Azure Active Directory Connect, w tym uaktualnienia w miejscu i migracji kierunku."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 31f084d8-2b89-478c-9079-76cf92e6618f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 57bd5b094654e4983cafa303b6f3daecadafb01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-a-previous-version-toohello-latest"></a>Azure AD Connect: Uaktualnianie z poprzedniej wersji toohello najnowsza wersja
W tym temacie opisano różne metody hello, których można używać tooupgrade Twojego połączenia usługi Azure Active Directory (Azure AD) instalacji toohello najnowszej wersji. Zaleca się pozostawienie samodzielnie bieżącego z wersjami hello programu Azure AD Connect. Można także użyć kroki hello w hello [migracji w kierunku](#swing-migration) sekcji podczas wprowadzania istotne zmiany konfiguracji.

Jeśli chcesz tooupgrade z narzędzia DirSync, zobacz [uaktualnienie z narzędzia Azure AD sync (DirSync)](active-directory-aadconnect-dirsync-upgrade-get-started.md) zamiast tego.

Istnieje kilka różne strategie, których można używać tooupgrade Azure AD Connect.

| Metoda | Opis |
| --- | --- |
| [Automatycznie uaktualnianie](active-directory-aadconnect-feature-automatic-upgrade.md) |Jest to najprostsza hello w przypadku klientów z instalacji ekspresowej. |
| [Uaktualnienie w miejscu](#in-place-upgrade) |Jeśli masz pojedynczego serwera, możesz uaktualnić hello instalacji w miejscu na hello na tym samym serwerze. |
| [Zasięg migracji](#swing-migration) |Przy użyciu dwóch serwerów przygotowanie jednego z serwerów hello z nową wersją hello lub konfiguracji i zmień hello aktywnego serwera, gdy wszystko jest gotowe. |

Aby uzyskać informacje o uprawnieniach, zobacz hello [uprawnienia wymagane do uaktualnienia](active-directory-aadconnect-accounts-permissions.md#upgrade).

> [!NOTE]
> Po włączeniu Twoje nowe Azure AD Connect serwera toostart synchronizowanie zmian tooAzure AD musi nie wycofasz toousing narzędzia DirSync i Azure AD Sync. Zmiana wersji na starszą od klientów toolegacy Azure AD Connect, łącznie z narzędzia DirSync i Azure AD Sync, nie jest obsługiwana i może prowadzić tooissues, takich jak utraty danych w usłudze Azure AD.

## <a name="in-place-upgrade"></a>Uaktualnienie w miejscu
Uaktualnienie w miejscu działa w przypadku przenoszenia z usługi Azure AD Sync lub Azure AD Connect. Ta funkcja nie działa z narzędzia DirSync lub rozwiązanie z programu Forefront Identity Manager (FIM) + Azure AD Connector.

Ta metoda jest preferowana pojedynczego serwera i mniejsza niż około 100 000 obiektów. Jeśli istnieją zmiany reguły synchronizacji out-of-box toohello, pełny import i pełną synchronizację wystąpić po uaktualnieniu hello. Ta metoda gwarantuje, że tej nowej konfiguracji hello jest stosowane tooall istniejące obiekty w systemie hello. Uruchom ten może potrwać kilka godzin w zależności od hello liczbę obiektów, które znajdują się w zakresie hello aparatu synchronizacji. Harmonogram synchronizacji normalne delta Hello (który domyślnie synchronizuje co 30 minut) jest wstrzymana, ale nadal synchronizacji haseł. Należy rozważyć sposób uaktualnienia w miejscu hello weekend. Jeśli nie ma żadnych zmian toohello out-of-box konfiguracji o hello nowej usługi Azure AD Connect wersji, następnie normalne import/synchronizacja różnicowa uruchamia zamiast tego.  
![Uaktualnienie w miejscu](./media/active-directory-aadconnect-upgrade-previous-version/inplaceupgrade.png)

Jeśli wprowadzono zmiany toohello synchronizacji out-of-box reguły następnie te reguły są cofnięcie toohello domyślnej konfiguracji w uaktualnieniu. toomake się upewnić, że konfigurację jest przechowywana między uaktualnień, upewnij się, wprowadzić zmiany, ponieważ są one opisane w [najlepsze rozwiązania dotyczące zmieniania konfiguracji domyślnej hello](active-directory-aadconnectsync-best-practices-changing-default-configuration.md).

Podczas uaktualniania w miejscu, mogą występować zmian wprowadzonych, które wymagają synchronizacji określonego działania (w tym kroki pełny Import i pełną synchronizację) toobe wykonywany po zakończeniu uaktualniania. toodefer takich działań można znaleźć toosection [jak toodefer pełnej synchronizacji po uaktualnieniu](#how-to-defer-full-synchronization-after-upgrade).

## <a name="swing-migration"></a>Migracja typu swing
Jeśli masz złożone wdrożenia lub wiele obiektów, może być niepraktyczne toodo uaktualnienia w miejscu, w systemie hello na żywo. W przypadku niektórych klientów ten proces może potrwać kilka dni — i w tym czasie nie zmiany różnicowe są przetwarzane. Tej metody można użyć również w przypadku planowania konfiguracji tooyour istotne zmiany toomake tootry ich limit przed ich jest wypychana toohello chmury.

zalecana metoda w tych scenariuszach Hello jest toouse migracji kierunku. Należy (co najmniej) dwa serwery — jeden serwer aktywnego i jeden serwer tymczasowej. Witaj aktywnego serwera (blue linia ciągła w hello poniższej ilustracji przedstawiono) jest odpowiedzialny za hello active produkcji obciążenia. powitania serwera (przedstawiono linie przerywane purpurowa) na potrzeby przemieszczania jest przygotowana z nową wersją hello lub konfiguracji. Gdy będzie gotowy pełni, ten serwer jest uaktywniona. Hello poprzedniej aktywnego serwera, który teraz ma hello starej wersji lub konfiguracji zainstalowane, staje się na serwerze tymczasowym hello i zostanie uaktualniony.

dwa serwery Hello możesz użyć innej wersji. Na przykład ASP hello zaplanowanie toodecommission można użyć usługi Azure AD Sync, a nowy serwer przemieszczania hello można używać usługi Azure AD Connect. Jeśli używasz opcji migracji toodevelop nową konfigurację, jego toohave dobrze hello tej samej wersji na hello dwa serwery.  
![Serwer przemieszczania](./media/active-directory-aadconnect-upgrade-previous-version/stagingserver1.png)

> [!NOTE]
> Niektórzy klienci preferują toohave trzech lub czterech serwerów dla tego scenariusza. Po uaktualnieniu serwera na potrzeby przemieszczania hello nie masz kopii zapasowej serwera dla [odzyskiwania po awarii](active-directory-aadconnectsync-operations.md#disaster-recovery). Przy użyciu trzech lub czterech serwerów można przygotować jednego zestawu serwerów podstawowych/w gotowości hello nowej wersji, która zapewnia, że jest zawsze przemieszczania serwera, który jest gotowy tootake za pośrednictwem.

Te kroki są również działać toomove z usługi Azure AD Sync lub rozwiązania z FIM + Azure AD Connector. Te kroki nie działają narzędzia DirSync, ale jest hello kroki tej samej zasięg metody migracji (nazywanych również wdrożenie równoległe) z narzędzia DirSync w [uaktualnienia usługi Azure Active Directory sync (DirSync)](active-directory-aadconnect-dirsync-upgrade-get-started.md).

### <a name="use-a-swing-migration-tooupgrade"></a>Użyj tooupgrade migracji zasięg
1. Jeśli używasz usługi Azure AD Connect na serwerach i Utwórz tooonly plan zmian w konfiguracji, upewnij się, że aktywnego serwera i serwerze są zarówno przy użyciu hello tej samej wersji. Dzięki temu łatwiej różnice toocompare później. Jeśli uaktualniasz z programu Azure AD Sync, te serwery mają różne wersje. Jeśli uaktualniasz ze starszej wersji programu Azure AD Connect jest dobrym rozwiązaniem toostart z hello dwa serwery, które są za pomocą hello tej samej wersji, ale nie jest to wymagane.
2. Jeśli wprowadzono niestandardowej konfiguracji i przemieszczania serwera nie ma go, wykonaj kroki hello w obszarze [przenieść Konfiguracja niestandardowa z toohello aktywnego serwera hello przemieszczania serwera](#move-custom-configuration-from-active-to-staging-server).
3. Jeśli uaktualniasz z wcześniejszych wersji programu Azure AD Connect, należy uaktualnić hello przemieszczania serwera toohello najnowszej wersji. Jeśli przenosisz z narzędzia Azure AD Sync, zainstaluj Azure AD Connect na serwerze tymczasowe.
4. Let hello synchronizacji aparat Uruchom pełny import i pełną synchronizację na serwerze tymczasowe.
5. Sprawdź, czy tej nowej konfiguracji hello nie spowodować nieoczekiwane zmiany przy użyciu kroków hello w obszarze "Zweryfikuj" w [hello Sprawdź konfigurację serwera](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server). Jeśli coś nie jest w oczekiwanym, poprawne, uruchom hello importowania i synchronizacji i sprawdź hello danych, dopóki wygląd, wykonując kroki hello.
6. Przełącz hello przemieszczania toobe hello aktywnego serwera. To ostatni krok hello "Przełącznika active server" w [hello Sprawdź konfigurację serwera](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server).
7. Jeśli uaktualniasz Azure AD Connect, należy uaktualnić serwer hello, który jest teraz tymczasowej w trybie toohello najnowszej wersji. Wykonaj kroki takie same jak przed tooget hello danych i konfiguracji uaktualnione hello. Po uaktualnieniu z programu Azure AD Sync, możesz teraz wyłączyć i zlikwidować stary serwer.

### <a name="move-a-custom-configuration-from-hello-active-server-toohello-staging-server"></a>Przenieś niestandardowej konfiguracji z hello active toohello przemieszczania serwera
Jeśli wprowadzono zmiany konfiguracji toohello aktywnego serwera należy toomake się, że które hello same zmiany zostaną zastosowane toohello przemieszczania serwera. Przenieś toohelp z tym, można użyć hello [Dokumentatora konfiguracji usługi Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).

Można przenieść hello synchronizacji niestandardowych reguł został utworzony przy użyciu programu PowerShell. Należy najpierw zastosować inne zmiany hello tak samo w obu systemów, a nie można migrować hello zmiany. Witaj [Dokumentatora konfiguracji](https://github.com/Microsoft/AADConnectConfigDocumenter) ułatwia porównanie hello dwa systemy toomake się, że są one identyczne. Narzędzie Hello może również pomóc w automatyzacji hello znaleziono w tej sekcji.

Potrzebujesz następujących hello tooconfigure rzeczy hello sam sposób na obu serwerach:

* Toohello połączenia tego samego lasów
* Domeny i jednostki Organizacyjnej filtrowania
* Witaj tej samej funkcji opcjonalnych, takich jak synchronizacja haseł i zapisywania zwrotnego haseł

**Przenoszenie reguł niestandardowych**  
Reguły niestandardowe synchronizacji toomove, hello następujące:

1. Otwórz **Edytor reguł synchronizacji** aktywnego serwera.
2. Wybierz regułę niestandardową. Kliknij przycisk **wyeksportować**. Spowoduje to wyświetlenie okna Notatnika. Zapisz plik tymczasowy hello z rozszerzeniem nazwy PS1. Dzięki temu skrypt programu PowerShell. Skopiuj toohello pliku PS1 hello przemieszczania serwera.  
   ![Wyeksportowanie reguły synchronizacji](./media/active-directory-aadconnect-upgrade-previous-version/exportrule.png)
3. Hello GUID łącznika różni się na powitania serwera na potrzeby przemieszczania i muszą go zmienić. start hello tooget identyfikator GUID, **Edytor reguł synchronizacji**, wybierz jedną z zasad out-of-box hello tego hello reprezentuje sama połączona systemu i kliknij przycisk **wyeksportować**. Zastąp hello identyfikatora GUID w pliku PS1 hello identyfikatora GUID z hello przemieszczania serwera.
4. W wierszu programu PowerShell Uruchom plik hello PS1. Spowoduje to utworzenie reguły synchronizacji niestandardowych hello na powitania serwera na potrzeby przemieszczania.
5. Powtórz tę czynność dla wszystkich reguł niestandardowych.

## <a name="how-toodefer-full-synchronization-after-upgrade"></a>Jak toodefer pełnej synchronizacji po uaktualnieniu
Podczas uaktualniania w miejscu, mogą występować zmian wprowadzonych, które wymagają synchronizacji określonego działania (w tym kroki pełny Import i pełną synchronizację) toobe wykonywane. Na przykład, wymagają zmian schematu łącznika **pełny import** wymagają zmian reguły synchronizacji krok i out-of-box **pełnej synchronizacji** krok toobe wykonane na zainfekowanym łączników. Podczas uaktualniania, Azure AD Connect Określa, jakie działania synchronizacji są wymagane i zapisuje je jako *zastępuje*. W hello następującego cyklu synchronizacji harmonogram synchronizacji hello przejmuje te zastąpienia i je wykonuje. Gdy przesłonięcie jest prawidłowo wykonane, zostanie ono usunięte.

Mogą wystąpić sytuacje, w którym nie ma miejsce tootake te zastąpienia natychmiast po uaktualnieniu. Na przykład masz wiele obiektów synchronizowanych i chcesz toooccur kroki te synchronizacji godzinami. tooremove te zastąpienia:

1. Podczas uaktualniania **Usuń zaznaczenie pola wyboru** hello opcja **Uruchom proces synchronizacji powitania po zakończeniu konfiguracji**. To wyłącza harmonogram synchronizacji hello i zapobiega cykl synchronizacji miejsce automatycznie przed zastąpienia hello są usuwane.

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync01.png)

2. Po zakończeniu uaktualniania, uruchom hello następującego polecenia cmdlet toofind się zastąpienia, które zostały dodane:`Get-ADSyncSchedulerConnectorOverride | fl`

   >[!NOTE]
   > zastąpienia Hello są specyficzne dla łącznika. W hello poniższy przykład, krok pełny Import i pełną synchronizację dodano tooboth hello AD łącznika lokalnego i łącznik usługi Azure AD.

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync02.png)

3. Należy zanotować hello istniejących zastąpień, które zostały dodane.
   
4. Witaj tooremove zastąpienia dla pełny import i pełną synchronizację łącznika dowolnego, uruchom następujące polecenie cmdlet hello:`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid-of-ConnectorIdentifier> -FullImportRequired $false -FullSyncRequired $false`

   tooremove hello zastąpień dla wszystkich łączników, wykonaj hello następującego skryptu programu PowerShell:

   ```
   foreach ($connectorOverride in Get-ADSyncSchedulerConnectorOverride)
   {
       Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier $connectorOverride.ConnectorIdentifier.Guid -FullSyncRequired $false -FullImportRequired $false
   }
   ```

5. tooresume hello harmonogramu, uruchom następujące polecenie cmdlet hello:`Set-ADSyncScheduler -SyncCycleEnabled $true`

   >[!IMPORTANT]
   > Należy pamiętać, kroki synchronizacji hello wymagane tooexecute najwcześniejszą wygodne. Możesz ręcznie wykonać te czynności przy użyciu hello Synchronization Service Manager lub dodać zastąpienia hello przy użyciu polecenia cmdlet Set-ADSyncSchedulerConnectorOverride hello.

Witaj tooadd zastąpienia dla pełny import i pełną synchronizację łącznika dowolnego, uruchom następujące polecenie cmdlet hello:`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid> -FullImportRequired $true -FullSyncRequired $true`

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
