---
title: "Monitorowanie synchronizacji danych Azure SQL z usługą OMS dziennika Analytics | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie monitorowania synchronizacji danych SQL Azure przy użyciu pakietu OMS analizy dzienników"
services: sql-database
ms.date: 11/7/2017
ms.topic: article
ms.service: sql-database
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ace0eb671556dc980836464a365731d6100eab25
ms.sourcegitcommit: bc8d39fa83b3c4a66457fba007d215bccd8be985
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2017
---
# <a name="monitor-sql-data-sync-preview-with-oms-log-analytics"></a>Synchronizacja danych SQL Monitor (wersja zapoznawcza) z pakietu OMS analizy dzienników 

Sprawdź dziennik aktywności synchronizacji danych SQL i wykrywać błędy i ostrzeżenia, należy wcześniej było ręcznie sprawdzić synchronizacji danych SQL w portalu Azure, lub użyj programu PowerShell lub interfejsu API REST. Wykonaj kroki opisane w tym artykule, aby skonfigurować niestandardowe rozwiązanie zwiększa monitorowania obsługi synchronizacji danych. Można dostosować to rozwiązanie do danego scenariusza.

Omówienie synchronizacji danych SQL, zobacz [synchronizacji danych między wieloma bazami danych chmury i lokalnych z synchronizacji danych SQL Azure (wersja zapoznawcza)](sql-database-sync-data.md).

## <a name="monitoring-dashboard-for-all-your-sync-groups"></a>Pulpit nawigacyjny monitorowania dla wszystkich grup synchronizacji 

Nie trzeba Przejrzyj dzienniki każdej grupy synchronizacji indywidualnie do wyszukania problemów. Wszystkie grupy synchronizacji można monitorować za pomocą dowolnego z subskrypcji w jednym miejscu, za pomocą widok niestandardowy OMS (Operations Management Suite). Ten widok udostępnia informacje, które ma znaczenie klientom synchronizacji danych SQL.

![Pulpitu nawigacyjnego monitorowania synchronizacji danych](media/sql-database-sync-monitor-oms/sync-monitoring-dashboard.png)

## <a name="automated-email-notifications"></a>Automatyczne powiadomienia E-mail

Nie trzeba sprawdzić dziennik ręcznie w portalu Azure lub za pomocą programu PowerShell lub interfejsu API REST. Z [analizy dzienników OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview), można tworzyć alerty, które go bezpośrednio na adresy e-mail osób, którym chcesz wyświetlać je po wystąpieniu błędu.

![Powiadomienia e-mail synchronizacji danych](media/sql-database-sync-monitor-oms/sync-email-notifications.png)

## <a name="how-do-you-set-up-these-monitoring-features"></a>Jak można skonfigurować te funkcje monitorowania? 

Implementowanie niestandardowych OMS, monitorowanie rozwiązania synchronizacji danych SQL w mniej niż godzinę, wykonując następujące czynności:

Należy skonfigurować trzy składniki:

-   Element runbook programu PowerShell ze źródłem danych dziennika SQL danych synchronizacji z usługą OMS.

-   Alert OMS analizy dzienników dla powiadomień e-mail.

-   Widok OMS do monitorowania.

### <a name="samples-to-download"></a>Przykłady do pobrania

Pobierz następujące dwa przykłady:

-   [Runbook programu PowerShell w dzienniku synchronizacji danych](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/sql-data-sync/DataSyncLogPowerShellRunbook.ps1)

-   [Widok OMS dziennika synchronizacji danych](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/sql-data-sync/DataSyncLogOmsView.omsview)

### <a name="prerequisites"></a>Wymagania wstępne

Upewnij się, że po skonfigurowaniu następujących czynności:

-   Konto usługi Automatyzacja Azure

-   Połączone z obszarem roboczym pakietu OMS analizy dzienników

## <a name="powershell-runbook-to-get-sql-data-sync-log"></a>Runbook programu PowerShell, aby uzyskać w dzienniku synchronizacji danych SQL 

Element runbook programu PowerShell hostowanych w usłudze Automatyzacja Azure umożliwia ściągania dziennika synchronizacji danych SQL, a następnie wysłać je z usługą OMS. Przykładowy skrypt jest dołączony. Warunkiem wstępnym musisz mieć konto usługi Automatyzacja Azure. Następnie należy utworzyć element runbook i zaplanuj jego uruchomienie. 

### <a name="create-a-runbook"></a>Tworzenie elementu runbook

Aby uzyskać więcej informacji na temat tworzenia elementu runbook, zobacz [Moje pierwszego elementu runbook programu PowerShell](https://docs.microsoft.com/azure/automation/automation-first-runbook-textual-powershell).

1.  Przy użyciu tego konta usługi Automatyzacja Azure, wybierz **elementów Runbook** kartę w obszarze automatyzacji procesu.

2.  Wybierz **Dodaj element Runbook** w lewym górnym rogu strony elementów Runbook.

3.  Wybierz **importowanie istniejącego elementu Runbook**.

4.  W obszarze **pliku Runbook**, użyj danego `DataSyncLogPowerShellRunbook` pliku. Ustaw **typ elementu Runbook** jako `PowerShell`. Nadaj nazwę elementu runbook.

5.  Wybierz pozycję **Utwórz**. Istnieje już element runbook.

6.  W obszarze Twoje konto usługi Automatyzacja Azure, wybierz **zmienne** kartę w obszarze udostępnionych zasobów.

7.  Wybierz **dodać zmienną** na zmienne. Utwórz zmienną do przechowywania ostatni czas wykonania elementu runbook. Jeśli masz wiele elementów runbook należy jedną zmienną dla każdego elementu runbook.

8.  Ustaw nazwę zmiennej jako `DataSyncLogLastUpdatedTime` i ustaw jej typ jako element DateTime.

9.  Wybierz element runbook, a następnie kliknij przycisk Edytuj w górnej części strony.

10. Zmiany wymagane do konta i konfiguracji synchronizacji danych SQL. (Aby uzyskać szczegółowe informacje, zobacz przykładowy skrypt).

    1.  Azure informacje.

    2.  Informacje o synchronizacji grupy.

    3.  Informacje o OMS. Te informacje można znaleźć w portalu OMS | Ustawienia | Połączonych źródeł. Aby uzyskać więcej informacji na temat wysyłania danych do analizy dzienników, zobacz [wysyłania danych do analizy dzienników przy użyciu protokołu HTTP danych modułu zbierającego interfejsu API (w publicznej wersji zapoznawczej)](../log-analytics/log-analytics-data-collector-api.md).

11. Uruchom element runbook w okienku testu. Sprawdź, czy było pomyślne.

    Jeśli masz błędy, upewnij się, że masz najnowszą zainstalowany moduł programu PowerShell. Można zainstalować moduł PowerShell najnowsze w **Galeria modułów** na Twoim koncie automatyzacji.

12. Kliknij przycisk **publikowania**

### <a name="schedule-the-runbook"></a>Planowanie elementu runbook

Aby zaplanować elementu runbook:

1.  W obszarze elementu runbook, zaznacz **harmonogramy** kartę w obszarze zasobów.

2.  Wybierz **Dodaj harmonogram** na stronie harmonogramów.

3.  Wybierz **Połącz harmonogram z elementem runbook**.

4.  Wybierz **Utwórz nowy harmonogram.**

5.  Ustaw **cyklu** cykliczny i ustaw interwał ma. Użyj tego samego interwału, skrypt i OMS.

6.  Wybierz pozycję **Utwórz**.

### <a name="check-the-automation"></a>Sprawdź automatyzacji

Można monitorować, czy Twoje automatyzacji działa zgodnie z oczekiwaniami, w obszarze **omówienie** Twojego konta automatyzacji, można znaleźć **statystyki zadania** wyświetlić w obszarze **monitorowanie**. Przypnij ten widok do pulpitu nawigacyjnego w celu łatwego wyświetlania. Uruchamia się pomyślnie Pokaż runbook jako "Ukończone" i działa wyświetlane jako "Nieudane".

## <a name="create-an-oms-log-reader-alert-for-email-notifications"></a>Utwórz Alert czytnika dziennika OMS powiadomień E-mail

Aby utworzyć alert, który używa analizy dzienników OMS, wykonaj następujące czynności. Jako warunek wstępny użytkownik musi być powiązany z obszarem roboczym pakietu OMS analizy dzienników.

1.  W portalu OMS wybierz **wyszukiwania dziennika**.

2.  Utwórz zapytanie, aby wybrać błędy i ostrzeżenia przez grupę synchronizacji z okresu wybranego. Na przykład:

    `Type=DataSyncLog\_CL LogLevel\_s!=Success| measure count() by SyncGroupName\_s interval 60minute`

3.  Po uruchomieniu kwerendy, wybierz informacją dzwonka **alertu**.

4.  W obszarze **Generowanie alertu na podstawie**, wybierz pozycję **metryki pomiaru**.

    1.  Ustawiono wartość zagregowaną **większa niż**.

    2.  Po **większa niż**, wprowadź wartość progową, którym chcesz otrzymywać powiadomienia. Oczekiwano błędów przejściowych w synchronizacji danych. Do zmniejszenia szumu, należy ustawić próg na wartość 5.

5.  W obszarze **akcje**ustaw **powiadomienia E-mail** "Yes". Wprowadź adresatów żądanej wiadomości e-mail.

6.  Kliknij pozycję **Zapisz**. Podanych odbiorców teraz otrzymywać powiadomienia pocztą e-mail, jeśli wystąpią błędy.

## <a name="create-an-oms-view-for-monitoring"></a>Tworzenie widoku OMS do monitorowania

Spowoduje to utworzenie widoku OMS wizualnie monitorowania wszystkich grup synchronizacji określony. Widok zawiera kilka składników:

-   Kafelka przeglądu, który pokazuje liczbę błędów, sukcesów i ostrzeżenia mają wszystkich grup synchronizacji.

-   Kafelek dla wszystkich grup synchronizacji, który informuje o liczbie błędów i ostrzeżeń dla każdej grupy synchronizacji. Grupy bez problemów nie są wyświetlane dla tego kafelka.

-   Kafelek dla każdej grupy synchronizacji pokazuje liczbę błędów, sukcesów i ostrzeżenia i ostatnie komunikaty o błędach.

Aby skonfigurować widok OMS, wykonaj następujące czynności:

1.  Na stronie głównej OMS wybierz plus po lewej stronie, aby otworzyć **Widok projektanta**.

2.  Wybierz **importu** na górnym pasku projektanta widoku. Następnie wybierz plik przykładowy "DataSyncLogOMSView".

3.  Przykładowy widok jest zarządzania dwie grupy synchronizacji. Edytuj ten widok, aby dopasować danego scenariusza. Kliknij przycisk **Edytuj** i wprowadź następujące zmiany:

    1.  Utwórz nowe obiekty "Lista & pierścień" z galerii zgodnie z potrzebami.

    2.  W każdej kafelka aktualizacji zapytania z informacjami.

        1.  W każdym segmencie zmienić interwał TimeStamp_t zgodnie z potrzebami.

        2.  Na Kafelki dla każdej grupy synchronizacji zaktualizuj nazwy grupy synchronizacji.

    3.  W każdym segmencie Zaktualizuj tytuł zgodnie z potrzebami.

4.  Kliknij przycisk **zapisać** i widoku jest gotowy.

## <a name="cost-of-this-solution"></a>Koszt tego rozwiązania

W większości przypadków to rozwiązanie jest bezpłatna.

**Automatyzacja Azure:** może być pewnych kosztów ponoszonych z kontem usługi Automatyzacja Azure, w zależności od użycie. 500 pierwszych minut zadanie było uruchamiane raz w każdym miesiącu jest bezpłatne. W większości przypadków to rozwiązanie powinien użyć mniej niż 500 minut miesięcznie. Aby uniknąć naliczania opłat, Zaplanuj uruchomienie elementu runbook w interwału dwie lub więcej godzin. Aby uzyskać więcej informacji, zobacz [cennik automatyzacji](https://azure.microsoft.com/pricing/details/automation/).

**Analiza dzienników OMS:** może być skojarzony z usługą OMS w zależności od użycie koszt. Warstwa bezpłatna obejmuje 500 MB danych pozyskiwane na dzień. W większości przypadków to rozwiązanie ma pozyskiwania mniej niż 500 MB na dzień. Aby zmniejszyć użycie, użyj tylko do awarii filtrowanie zawarte w elemencie runbook. Jeśli używasz więcej niż 500 MB na dzień, Uaktualnij do planu płatną, aby uniknąć zagrożenia analytics zatrzymywanie po osiągnięciu ograniczenia. Aby uzyskać więcej informacji, zobacz [cennik analizy dzienników](https://azure.microsoft.com/pricing/details/log-analytics/).

## <a name="code-samples"></a>Przykłady kodu

Pobierz przykłady kodu, opisane w tym artykule w następujących lokalizacjach:

-   [Runbook programu PowerShell w dzienniku synchronizacji danych](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/sql-data-sync/DataSyncLogPowerShellRunbook.ps1)

-   [Widok OMS dziennika synchronizacji danych](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/sql-data-sync/DataSyncLogOmsView.omsview)

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat synchronizacji danych SQL zobacz:

-   [Synchronizowanie danych w wielu w chmurze i lokalnych baz danych z synchronizacji danych SQL Azure](sql-database-sync-data.md)
-   [Konfigurowanie synchronizacji danych SQL Azure](sql-database-get-started-sql-data-sync.md)
-   [Najlepsze rozwiązania dotyczące synchronizacji danych SQL Azure](sql-database-best-practices-data-sync.md)
-   [Rozwiązywanie problemów z synchronizacją danych SQL Azure](sql-database-troubleshoot-data-sync.md)

-   Wykonaj przykłady z programu PowerShell, które przedstawiają sposób konfigurowania synchronizacji danych SQL:
    -   [Synchronizacja między wiele baz danych Azure SQL przy użyciu programu PowerShell](scripts/sql-database-sync-data-between-sql-databases.md)
    -   [Synchronizacja między bazą danych SQL Azure i lokalnej bazy danych programu SQL Server przy użyciu programu PowerShell](scripts/sql-database-sync-data-between-azure-onprem.md)

-   [Pobrać dokumentację interfejsu API REST synchronizacji danych SQL](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)

Aby uzyskać więcej informacji na temat bazy danych SQL zobacz:

-   [Omówienie bazy danych SQL](sql-database-technical-overview.md)
-   [Zarządzanie cyklem życia bazy danych](https://msdn.microsoft.com/library/jj907294.aspx)
