---
title: aaaGetting wprowadzenie zadania elastycznej bazy danych | Dokumentacja firmy Microsoft
description: jak toouse zadania elastycznej bazy danych
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 2540de0e-2235-4cdd-9b6a-b841adba00e5
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: bc5894d2df4235738ab961db4f69c11cdf786cc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-elastic-database-jobs"></a>Wprowadzenie zadania elastycznej bazy danych
Zadania elastyczne bazy danych (wersja zapoznawcza) dla bazy danych SQL Azure umożliwia tooreliability wykonywanie skryptów T-SQL, obejmującej wiele baz danych podczas automatycznym ponowieniem próby i zapewnianie ostatecznego zakończenia gwarancji. Aby uzyskać więcej informacji na temat funkcji zadania elastycznej bazy danych hello Zobacz hello [strony Przegląd funkcji](sql-database-elastic-jobs-overview.md).

W tym temacie rozszerza próbki hello w [wprowadzenie do korzystania z narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md). Po zakończeniu zostanie: Dowiedz się, jak toocreate zadania, które zarządzają grupy powiązanych baz danych i zarządzać nimi. Nie jest wymagane toouse hello elastycznego skalowania narzędzi w kolejności tootake korzystając z zalet hello zadania elastyczne.

## <a name="prerequisites"></a>Wymagania wstępne
Pobierz i uruchom hello [wprowadzenie próbki narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a>Tworzenie mapy niezależnego fragmentu manager za pomocą hello przykładowej aplikacji
W tym miejscu spowoduje utworzenie mapy niezależnego fragmentu manager oraz kilka fragmentów, następuje wstawiania danych do odłamków hello. Jeśli masz już skonfigurowano w nich danych podzielonej odłamków, można pominąć hello następujące kroki i przenieść toohello następnej sekcji.

1. Tworzenie i uruchamianie hello **wprowadzenie do korzystania z narzędzi elastycznej bazy danych** przykładowej aplikacji. Wykonaj kroki hello aż do kroku 7 w sekcji hello [pobieranie i uruchamianie aplikacji przykładowej hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app). Na końcu hello kroku 7 zostanie wyświetlony hello następującego wiersza polecenia:

   ![Wiersz polecenia](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. W oknie polecenia hello, wpisz "1", a następnie naciśnij klawisz **Enter**. Tworzy menedżera map niezależnego fragmentu hello i dodaje dwa niezależne toohello serwera. Następnie wpisz "3" i naciśnij klawisz **Enter**; Powtarzaj tę akcję, cztery razy. Wstawia Przykładowe wiersze danych z fragmentów.
3. Witaj [Azure Portal](https://portal.azure.com) powinny być widoczne trzech nowych baz danych:

   ![Visual Studio potwierdzenia](./media/sql-database-elastic-query-getting-started/portal.png)

   W tym momencie utworzymy odzwierciedla wszystkie hello bazy danych na mapie niezależnego fragmentu hello kolekcji niestandardowej bazie danych. Spowoduje to zezwolić nam toocreate i wykonać zadanie, które Dodaj nową tabelę między fragmentów.

W tym miejscu będą zazwyczaj utworzymy obiektu docelowego mapy niezależnego fragmentu przy użyciu hello **AzureSqlJobTarget nowy** polecenia cmdlet. Hello niezależnego fragmentu Mapa menedżera z bazy danych musi być ustawiona jako docelowej bazy danych, a następnie mapy określonych niezależnych hello jest określony jako element docelowy. Zamiast tego firma Microsoft będzie tooenumerate wszystkich hello baz danych na serwerze hello a Dodaj hello baz danych toohello nowej niestandardowej kolekcji z wyjątkiem hello bazy danych master.

## <a name="creates-a-custom-collection-and-add-all-databases-in-hello-server-toohello-custom-collection-target-with-hello-exception-of-master"></a>Tworzy kolekcję niestandardową, a następnie dodaj wszystkie bazy danych w lokalizacji docelowej kolekcji niestandardowej toohello serwera hello z wyjątkiem hello wzorca.
   ```
    $customCollectionName = "dbs_in_server"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $ResourceGroupName = "ddove_samples"
    $ServerName = "samples"
    $dbsinserver = Get-AzureRMSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName
    $dbsinserver | %{
    $currentdb = $_.DatabaseName
    $ErrorActionPreference = "Stop"
    Write-Output ""

    Try
    {
       New-AzureSqlJobTarget -ServerName $ServerName -DatabaseName $currentdb | Write-Output
    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already a database target."
        }

        else
        {
            throw $_
        }

    }

    Try
    {
        if ($currentdb -eq "master")
        {
            Write-Host $currentdb "will not be added custom collection target" $CustomCollectionName "."
        }

        else
        {
            Add-AzureSqlJobChildTarget -CustomCollectionName $CustomCollectionName -ServerName $ServerName -DatabaseName $currentdb
            Write-Host $currentdb "was added to" $CustomCollectionName "."
        }

    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already in hello custom collection target" $CustomCollectionName"."
        }

        else
        {
            throw $_
        }
    }
    $ErrorActionPreference = "Continue"
   }
   ```
## <a name="create-a-t-sql-script-for-execution-across-databases"></a>Tworzenie skryptu T-SQL do wykonania dla baz danych
   ```
    $scriptName = "NewTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'Test')
    BEGIN
        CREATE TABLE Test(
            TestId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO Test(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script
   ```

## <a name="create-hello-job-tooexecute-a-script-across-hello-custom-group-of-databases"></a>Utwórz skrypt tooexecute zadania hello między hello niestandardową grupę baz danych

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-hello-job"></a>Wykonanie zadania hello
Hello następującego skryptu programu PowerShell może być używane tooexecute istniejącego zadania:

Aktualizacja hello następującej zmiennej tooreflect hello żądanego zadania nazwa toohave wykonane:

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-hello-state-of-a-single-job-execution"></a>Pobiera stan hello wykonywania pojedyncze zadanie
Użyj hello sam **Get-AzureSqlJobExecution** polecenia cmdlet z hello **właściwość IncludeChildren** parametru tooview hello stan wykonania zadania podrzędne, czyli hello określonym stanie dla każdego wykonywania zadania w odniesieniu do każdego celem zadania hello bazy danych.

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-hello-state-across-multiple-job-executions"></a>Wyświetlanie stanu hello między wieloma wykonania zadania
Witaj **Get AzureSqlJobExecution** polecenie cmdlet ma wiele parametrów opcjonalnych, które mogą być używane toodisplay wielu wykonania zadania, filtrowane przez hello podane parametry. Hello poniżej przedstawiono niektóre hello możliwości toouse Get-AzureSqlJobExecution:

Pobierz wszystkie aktywne najwyższego poziomu zadanie wykonaniami:

   ```
    Get-AzureSqlJobExecution
   ```

Pobierz wszystkie wykonaniami najwyższego poziomu zadania, w tym wykonaniami nieaktywnego zadania:

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

Pobierz wszystkie wykonania zadania podrzędne identyfikatora wykonywania podane zadanie wykonaniami nieaktywnego zadania w tym:

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

Pobierz wszystkie wykonania zadania utworzone za pomocą harmonogramu / zadania kombinacji, w tym nieaktywnych zadań:

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

Pobieranie wszystkich zadań przeznaczonych dla określonej niezależnych mapy, w tym nieaktywnych zadań:

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

Pobieranie wszystkich zadań przeznaczonych dla określonej kolekcji niestandardowych, łącznie z nieaktywnych zadań:

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

Pobrać listy hello zadanie wykonania zadania w ramach wykonania określonego zadania:

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

Pobieranie szczegółów wykonywania zadań zadania:

Witaj następującego skryptu programu PowerShell może być używane tooview hello szczegóły zadania wykonywania zadań, które jest szczególnie przydatne w przypadku debugowania awarii wykonywania.
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a>Pobrać błędów w ramach zadania wykonania zadania
Obiekt JobTaskExecution Hello zawiera właściwość dla cyklu życia zadania hello wraz z właściwością wiadomość hello. Jeżeli wykonanie zadania zadania nie powiodło się, hello cyklu życia właściwość zostanie ustawiona zbyt** i właściwości wiadomości powitania ustawi toohello Wynikowy komunikat o wyjątku i jego stosu. Jeśli zadanie nie powiodło się, jest ważne tooview hello szczegóły zadania, których nie powiodła się dla danego zadania.

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions)
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }
   ```

## <a name="waiting-for-a-job-execution-toocomplete"></a>Oczekiwanie na toocomplete wykonania zadania
Hello następującego skryptu programu PowerShell może być używane toowait dla toocomplete zadań zadania:

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a>Tworzenie zasad wykonywania niestandardowych
Zadania elastyczne bazy danych obsługuje tworzenie zasad wykonywania niestandardowych, które mogą być stosowane podczas uruchamiania zadania.

Zasady wykonywania obecnie umożliwiają definiowanie:

* Name: Identyfikator hello zasad wykonywania.
* Limit czasu zadania: Całkowity czas przed zadania zostaną anulowane przez zadania elastyczne bazy danych.
* Interwał ponawiania prób początkowej: Interwał toowait przed ponowną próbą wykonania pierwszej.
* Maksymalny interwał ponawiania: Limit toouse interwałów ponów próbę.
* Współczynnik wycofywania interwału ponawiania: Współczynnik używany toocalculate hello dalej interwał między ponownymi próbami.  Witaj używana jest następująca formuła: (początkowej interwał ponawiania próby) * Math.Pow — ((interwał wycofywania współczynnik) (liczba prób) - 2).
* Maksymalna liczba prób: hello maksymalna liczba ponawiania prób tooperform w ramach danego zadania.

domyślne zasady wykonywania Hello używa hello następujące wartości:

* Nazwa: Domyślne zasady wykonywania
* Limit czasu zadania: 1 tydzień
* Interwał ponawiania prób początkowej: 100 milisekund
* Maksymalny interwał ponawiania: 30 minut
* Spróbuj ponownie współczynnik interwał: 2
* Maksymalna liczba prób: 2 147 483 647

Tworzenie zasad wykonywania hello potrzeby:

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy
   ```

### <a name="update-a-custom-execution-policy"></a>Aktualizacja zasad wykonywania niestandardowych
Aktualizacja hello potrzeby tooupdate zasad wykonywania:

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy
   ```

## <a name="cancel-a-job"></a>Anulowanie zadania
Zadania elastyczne bazy danych obsługuje żądania anulowania zadań.  Jeśli zadania elastyczne bazy danych wykryje żądanie anulowania aktualnie wykonywanego zadania, podejmie toostop hello zadania.

Istnieją dwa różne sposoby, że zadania elastyczne bazy danych można wykonać anulowania:

1. Anulowanie aktualnie wykonywanych zadań: wykrycie anulowania aktualnie uruchomionej zadania anulowania będą podejmowane w hello aktualnie wykonywanych aspekt hello zadań.  Na przykład: w przypadku długo działające kwerendy obecnie wykonywana jest próba anulowania, nastąpi próba toocancel hello zapytania.
2. Anulowanie zadań ponownych prób: W przypadku anulowania wykrycia przez wątek kontroli hello przed uruchomieniu zadania do wykonania, hello kontroli wątku będzie uniknąć uruchamiania zadań hello i zadeklarować żądania hello jak anulowane.

Jeśli żądanie anulowania zadań dla zadania nadrzędnego, żądanie anulowania hello będą honorowane dla zadania nadrzędnego hello i wszystkich jego zadań podrzędnych.

toosubmit żądanie anulowania, użyj hello **Stop-AzureSqlJobExecution** polecenia cmdlet i zestaw hello **JobExecutionId** parametru.

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-hello-jobs-history"></a>Usuwanie zadania według nazwy i historii zadań hello
Zadania elastyczne bazy danych obsługuje asynchroniczne usuwania. Zadanie może być oznaczony do usunięcia, a hello system spowoduje usunięcie hello zadania i jego historii zadań po zakończeniu wszystkich zadań wykonaniami hello zadania. Witaj systemu nie będzie automatycznie anulowania wykonaniami aktywnego zadania.  

Zamiast tego Stop-AzureSqlJobExecution musi być wywołana toocancel wykonaniami aktywnego zadania.

Usuwanie zadania tootrigger, użyj hello **AzureSqlJob Usuń** polecenia cmdlet i zestaw hello **JobName** parametru.

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a>Tworzenie obiektu docelowego w niestandardowej bazie danych
Obiekty docelowe w niestandardowej bazie danych można zdefiniować w zadania elastycznej bazy danych, które mogą być używane do wykonywania bezpośrednio lub dołączania w ramach grupy niestandardowej bazy danych. Ponieważ **pule elastyczne** nie są jeszcze bezpośrednio obsługiwane za pośrednictwem hello interfejsów API programu PowerShell, należy po prostu utworzyć obiekt docelowy w niestandardowej bazie danych oraz miejsca docelowego do kolekcji niestandardowej bazy danych, które obejmuje wszystkie hello bazy danych w puli hello.

Ustaw hello następujące zmienne tooreflect hello potrzeby bazy danych:

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a>Utwórz docelowy kolekcji niestandardowej bazy danych
Docelowy kolekcji niestandardowej bazy danych może być wykonanie tooenable zdefiniowanych przez wiele obiektów docelowych określonych bazy danych. Po utworzeniu grupy bazy danych, baz danych może być skojarzony toohello docelowej kolekcji niestandardowej.

Ustaw powitania po konfiguracji docelowej żądanej kolekcji niestandardowych zmiennych tooreflect hello:

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-tooa-custom-database-collection-target"></a>Dodawanie baz danych tooa w niestandardowej bazie danych kolekcji docelowego
Obiekty docelowe bazy danych może być skojarzony z niestandardowej bazie danych kolekcji elementów docelowych toocreate grupę baz danych. Zawsze, gdy tworzone jest zadanie cel kolekcji niestandardowej bazy danych, będzie tootarget rozwinięte hello bazy danych skojarzony toohello grupy w momencie hello wykonywania.

Dodaj określonej kolekcji niestandardowych hello potrzeby bazy danych tooa:

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a>Przejrzyj hello bazy danych, w docelowej kolekcji niestandardowej bazy danych
Użyj hello **Get-AzureSqlJobTarget** polecenia cmdlet tooretrieve hello podrzędnej bazy danych, w docelowej kolekcji niestandardowej bazie danych.

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a>Utwórz skrypt tooexecute zadania w docelowej kolekcji niestandardowej bazy danych
Użyj hello **AzureSqlJob nowy** toocreate polecenia cmdlet zadania przed grupę baz danych, wynika z docelowej kolekcji niestandardowej bazie danych. Zadania elastyczne bazy danych będzie rozszerzać hello zadania do wielu zadań podrzędnych każdego odpowiednia baza danych tooa skojarzone z hello w niestandardowej bazie danych kolekcji docelowych i upewnij się, że hello skrypt zostanie wykonany w każdej bazie danych. Ponownie ważne jest, że skrypty są odporne tooretries toobe idempotentności.

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a>Zbieranie danych dla baz danych
**Zadania elastyczne bazy danych** obsługuje wykonywanie zapytania na grupę baz danych i wysyła hello wyniki tooa określonej tabeli bazy danych. Witaj tabeli może być badana po hello fakt toosee hello wyniki zapytania w każdej bazie danych. Zapewnia to tooexecute asynchronicznego mechanizmu zapytania przez wiele baz danych. Błąd przypadkach, takich jak jednej z baz danych hello są tymczasowo niedostępne są obsługiwane automatycznie za pośrednictwem ponownych prób.

Witaj określonej lokalizacji docelowej tabeli będą tworzone automatycznie, jeśli jeszcze nie istnieje, zgodnego schematu hello hello zwrócił zestaw wyników. Jeśli wykonanie skrypt zwraca wiele zestawów wyników, zadania elastycznej bazy danych wysyła hello pierwszy toohello co podane tabeli docelowej.

Witaj następującego skryptu programu PowerShell może być używane tooexecute skrypt zbieranie jej wyników do określonej tabeli. Ten skrypt założono, że utworzono skryptu T-SQL, który generuje pojedynczy zestaw wyników i docelowej kolekcji niestandardowej bazie danych została utworzona.

Ustaw powitania po tooreflect skryptu hello potrzeby, poświadczenia i wykonywania obiekt docelowy:

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a>Tworzenie i uruchamianie zadania dla scenariuszy zbierania danych
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a>Utwórz harmonogram wykonywania zadania przy użyciu wyzwalacz zadania
Witaj następującego skryptu programu PowerShell może być używane toocreate reoccurring harmonogramu. Ten skrypt używa interwał jedną minutę, ale nowy AzureSqlJobSchedule obsługuje również parametry - DayInterval, - HourInterval i - MonthInterval, - WeekInterval. Można utworzyć harmonogramy, które są wykonywane tylko raz przekazywanie przez - jednorazowe.

Utwórz nowy harmonogram:
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-toohave-a-job-executed-on-a-time-schedule"></a>Utwórz zadanie wykonywane zgodnie z harmonogramem czasu toohave wyzwalacz zadania
Wyzwalacz zadania mogą być zdefiniowane toohave zgodnie z zadania wykonywane harmonogram tooa. Witaj następującego skryptu programu PowerShell może być używane toocreate wyzwalacza zadania.

Ustaw hello następujące zmienne toocorrespond toohello żądanego zadania i harmonogramu:

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a>Usuń skojarzenie zaplanowane zadanie toostop wykonywanie zgodnie z harmonogramem
można usunąć toodiscontinue pojawiał wykonywania zadań za pomocą wyzwalacza zadania hello wyzwalacza zadania.
Usuwanie zadania toostop wyzwalacz zadania wykonywane zgodnie z harmonogramem tooa przy użyciu hello **AzureSqlJobTrigger Usuń** polecenia cmdlet.

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-tooexcel"></a>Importuj tooExcel wyników zapytania elastycznej bazy danych
 Możesz zaimportować hello wyników z pliku programu Excel tooan zapytania.

1. Uruchom program Excel 2013.
2. Przejdź toohello **danych** wstążki.
3. Kliknij przycisk **z innych źródeł** i kliknij przycisk **z programu SQL Server**.

   ![Importowania z programu Excel z innych źródeł](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. W hello **Kreator połączenia danych** wpisz powitania serwera nazwę i poświadczenia logowania. Następnie kliknij przycisk **Next** (Dalej).
5. W oknie dialogowym hello **hello wybierz bazy danych, która zawiera dane hello**, wybierz pozycję hello **ElasticDBQuery** bazy danych.
6. Wybierz hello **klientów** tabeli w widoku listy hello, a następnie kliknij przycisk **dalej**. Następnie kliknij przycisk **Zakończ**.
7. W hello **i zaimportuj dane** formularza, w obszarze **wybierz sposób tooview tych danych w skoroszycie**, wybierz pozycję **tabeli** i kliknij przycisk **OK**.

Witaj wszystkie wiersze z **klientów** tabeli, przechowywane w różnych odłamków wypełnić hello arkuszu programu Excel.

## <a name="next-steps"></a>Następne kroki
Możesz teraz użyć funkcji danych programu Excel. Użyj parametrów połączenia hello nazwę serwera, nazwa bazy danych i poświadczeń tooconnect BI i dane integracji narzędzia toohello zapytania elastycznej bazy danych. Upewnij się, czy program SQL Server jest obsługiwana jako źródło danych dla własnych narzędzi. Znajdują się toohello elastycznej zapytanie do bazy danych i tabele zewnętrzne, podobnie jak wszystkie inne bazy danych programu SQL Server i czy można połączyć toowith własnych narzędzi tabel programu SQL Server.

### <a name="cost"></a>Koszty
Brak bez dodatkowych opłat dla funkcji zapytania hello elastycznej bazy danych. Jednak w tej chwili ta funkcja jest dostępna tylko w bazach danych premium jako punkt końcowy, ale odłamków hello może być dowolnym warstwy usługi.

Aby uzyskać informacje o cenach zobacz [szczegóły cennika bazy danych SQL](https://azure.microsoft.com/pricing/details/sql-database/).

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
