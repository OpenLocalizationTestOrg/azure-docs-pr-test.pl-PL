---
title: "Azure AD Connect: Jak ograniczyć toorecover z LocalDB 10GB problem | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano, jak toorecover Azure AD Connect synchronizacji usługi po napotkaniu LocalDB 10GB ograniczyć problem."
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 41d081af-ed89-4e17-be34-14f7e80ae358
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 7b8ce6e19b68837639017bb0315eda4b924d525a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-how-toorecover-from-localdb-10-gb-limit"></a>Azure AD Connect: Jak toorecover z LocalDB limitu 10 GB
Azure AD Connect wymaga danych tożsamości toostore bazy danych programu SQL Server. Można używał domyślnego hello programu SQL Server 2012 Express LocalDB zainstalowane z programem Azure AD Connect lub użyć własnych pełne SQL. Program SQL Server Express narzuca limit rozmiaru w wysokości 10 GB. Jeśli jest używany program LocalDB i limit zostanie osiągnięty, usługa synchronizacji programu Azure AD Connect nie będzie mogła uruchomić się ani prawidłowo wykonywać synchronizacji. W tym artykule przedstawiono kroki odzyskiwania hello.

## <a name="symptoms"></a>Objawy
Istnieją dwa wspólne symptomy:

* Azure AD Connect usługi synchronizacji **działa** , ale nie powiedzie się toosynchronize z *"zatrzymana-bazy danych dysk pełny"* błędu.

* Azure AD Connect usługi synchronizacji **toostart jest**. Podczas próby toostart hello usługi pojawia się błąd zdarzeń 6323 i komunikat o błędzie *"hello serwer napotkał błąd, ponieważ serwer SQL jest mało miejsca na dysku."*

## <a name="short-term-recovery-steps"></a>Procedura odzyskiwania krótkoterminowego
W tej sekcji miejsce hello kroki tooreclaim bazy danych wymaganych przez operację tooresume Azure AD Connect usługi synchronizacji. Witaj kroki obejmują:
1. [Sprawdź stan usługi synchronizacji hello](#determine-the-synchronization-service-status)
2. [Zmniejszanie hello bazy danych](#shrink-the-database)
3. [Usuwanie danych w historii](#delete-run-history-data)
4. [Skrócić okres przechowywania danych historii wykonywania](#shorten-retention-period-for-run-history-data)

### <a name="determine-hello-synchronization-service-status"></a>Sprawdź stan usługi synchronizacji hello
Po pierwsze należy ustalić, czy hello usługi synchronizacji nadal jest uruchomiona lub nie:

1. Zaloguj się za tooyour serwera Azure AD Connect jako administrator.

2. Przejdź za**Menedżera sterowania usługami**.

3. Sprawdź stan hello **Microsoft Azure AD Sync**.


4. Jeśli została uruchomiona, nie zatrzymać lub ponownie uruchom usługę hello. Pomiń [bazy danych hello zmniejszania](#shrink-the-database) krok i przejdź zbyt[Delete Uruchom historyczne dane](#delete-run-history-data) kroku.

5. Jeśli nie jest uruchomiona, spróbuj toostart hello usługi. Jeśli pomyślnym uruchomieniu usługi hello, Pomiń [bazy danych hello zmniejszania](#shrink-the-database) krok i przejdź zbyt[Delete Uruchom historyczne dane](#delete-run-history-data) krok. W przeciwnym razie kontynuuj [bazy danych hello zmniejszania](#shrink-the-database) kroku.

### <a name="shrink-hello-database"></a>Zmniejszanie hello bazy danych
Użyj toofree operacji zmniejszania hello się wystarczająco dużo hello toostart miejsca bazy danych usługi synchronizacji. Zwalnia jego miejsce DB przez usunięcie odstępy w bazie danych hello. Ten krok jest optymalnych, ponieważ nie gwarantuje, że zawsze przeprowadza odzyskiwanie miejsca. toolearn więcej informacji na temat operacji zmniejszania, przeczytaj ten artykuł [baza danych](https://msdn.microsoft.com/library/ms189035.aspx).

> [!IMPORTANT]
> Pomiń ten krok, jeśli zostanie wyświetlony hello toorun usługi synchronizacji. Nie zaleca hello tooshrink bazy danych SQL, ponieważ może to prowadzić wydajności toopoor powodu fragmentacji tooincreased.

Nazwa Hello hello bazy danych utworzone dla usługi Azure AD Connect jest **ADSync**. tooperform operację zmniejszania, należy zalogować się jako hello sysadmin lub DBO hello bazy danych. Podczas instalacji usługi Azure AD Connect hello następujące konta mają prawa administratora systemu:
* Administratorzy lokalni
* Hello konto użytkownika, który był używany toorun usługi Azure AD Connect instalacji.
* Witaj konta usługi synchronizacji, który jest używany jako hello działających w kontekście usługi Azure AD Connect synchronizacji.
* grupy lokalne powitania ADSyncAdmins, który został utworzony podczas instalacji.

1. Utwórz kopię zapasową bazy danych hello przez skopiowanie **ADSync.mdf** i **ADSync_log.ldf** pliki znajdujące się w obszarze `%ProgramFiles%\program files\Microsoft Azure AD Sync\Data` tooa bezpiecznej lokalizacji.

2. Rozpocznij nową sesję programu PowerShell.

3. Przejdź toofolder `%ProgramFiles%\Program Files\Microsoft SQL Server\110\Tools\Binn`.

4. Uruchom **sqlcmd** narzędzia, uruchamiając polecenie hello `./SQLCMD.EXE -S “(localdb)\.\ADSync” -U <Username> -P <Password>`, przy użyciu poświadczeń hello sysadmin lub hello bazy danych DBO.

5. tooshrink hello bazy danych w wierszu polecenia sqlcmd hello (1 >), wprowadź `DBCC Shrinkdatabase(ADSync,1);`, a następnie `GO` w następnym wierszu hello.

6. Jeśli operacja hello powiedzie się, spróbuj ponownie hello toostart usługi synchronizacji. Jeśli można uruchomić hello usługi synchronizacji, przejdź zbyt[Delete Uruchom dane historii](#delete-run-history-data) kroku. Jeśli nie, skontaktuj się z pomocą techniczną.

### <a name="delete-run-history-data"></a>Usuwanie danych w historii
Domyślnie program Azure AD Connect przechowuje tooseven dni, przez które Historia uruchomień danych. W tym kroku usunąć hello Uruchom historii danych tooreclaim DB miejsca tak, aby uruchomić usługi Azure AD Connect usługi synchronizacji ponownie przeprowadzić synchronizację.

1.  Uruchom **Menedżera usługi synchronizacji** przez przejście → tooSTART usługi synchronizacji.

2.  Przejdź toohello **operacji** kartę.

3.  W obszarze **akcje**, wybierz pozycję **uruchamia wyczyść**...

4.  Możesz wybrać **wyczyść wszystkie elementy** lub **wyczyść jest uruchamiany przed... <date>**  opcji. Zaleca się uruchamiania czyszcząc Uruchom historyczne dane, które są starsze niż dwa dni. Jeśli będziesz kontynuować toorun do problem rozmiar bazy danych, a następnie wybierz hello **wyczyść wszystkie elementy** opcji.

### <a name="shorten-retention-period-for-run-history-data"></a>Skrócić okres przechowywania danych historii wykonywania
Ten krok jest tooreduce hello prawdopodobieństwo powodowania hello limitu 10 GB problem po wielu cykli synchronizacji.

1. Otwórz nową sesję programu PowerShell.

2. Uruchom `Get-ADSyncScheduler` i zwróć uwagę na powitania PurgeRunHistoryInterval właściwość, która określa hello bieżącego okresu przechowywania.

3. Uruchom `Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00` dni tootwo okresu przechowywania hello tooset. Dostosuj okres przechowywania hello zależnie od potrzeb.

## <a name="long-term-solution--migrate-toofull-sql"></a>Rozwiązanie do długoterminowego — toofull migracji SQL
Ogólnie rzecz biorąc, problem hello jest świadczy, że rozmiar 10 GB bazy danych nie jest już umożliwiający toosynchronize Azure AD Connect z lokalnej usługi Active Directory tooAzure AD. Zalecane jest, aby przełączyć toousing hello pełnej wersji programu SQL server. Nie można bezpośrednio zamienić hello LocalDB istniejącego wdrożenia usługi Azure AD Connect z bazą danych hello hello pełnej wersji programu SQL Server. Zamiast tego należy wdrożyć na nowy serwer Azure AD Connect z hello pełnej wersji programu SQL Server. Zaleca się przeprowadzić migrację zasięg, wdrożonym hello nowy serwer Azure AD Connect (z bazy danych SQL) jako serwer przemieszczania dalej toohello istniejącego Azure AD Connect serwera (za pomocą LocalDB). 
* Aby uzyskać instrukcje dotyczące sposobu tooconfigure zdalnego SQL z programem Azure AD Connect, zobacz tooarticle [Instalacja niestandardowa programu Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom).
* Aby uzyskać instrukcje dotyczące migracji zasięg dla uaktualnianie programu Azure AD Connect, można znaleźć tooarticle [Azure AD Connect: uaktualnianie z poprzedniej wersji toohello najnowszych](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#swing-migration).

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
