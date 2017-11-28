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
# <a name="getting-started-with-elastic-database-jobs"></a><span data-ttu-id="decc6-103">Wprowadzenie zadania elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="decc6-103">Getting started with Elastic Database jobs</span></span>
<span data-ttu-id="decc6-104">Zadania elastyczne bazy danych (wersja zapoznawcza) dla bazy danych SQL Azure umożliwia tooreliability wykonywanie skryptów T-SQL, obejmującej wiele baz danych podczas automatycznym ponowieniem próby i zapewnianie ostatecznego zakończenia gwarancji.</span><span class="sxs-lookup"><span data-stu-id="decc6-104">Elastic Database jobs (preview) for Azure SQL Database allows you tooreliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span></span> <span data-ttu-id="decc6-105">Aby uzyskać więcej informacji na temat funkcji zadania elastycznej bazy danych hello Zobacz hello [strony Przegląd funkcji](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="decc6-105">For more information about hello Elastic Database job feature, please see hello [feature overview page](sql-database-elastic-jobs-overview.md).</span></span>

<span data-ttu-id="decc6-106">W tym temacie rozszerza próbki hello w [wprowadzenie do korzystania z narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="decc6-106">This topic extends hello sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span> <span data-ttu-id="decc6-107">Po zakończeniu zostanie: Dowiedz się, jak toocreate zadania, które zarządzają grupy powiązanych baz danych i zarządzać nimi.</span><span class="sxs-lookup"><span data-stu-id="decc6-107">When completed, you will: learn how toocreate and manage jobs that manage a group of related databases.</span></span> <span data-ttu-id="decc6-108">Nie jest wymagane toouse hello elastycznego skalowania narzędzi w kolejności tootake korzystając z zalet hello zadania elastyczne.</span><span class="sxs-lookup"><span data-stu-id="decc6-108">It is not required toouse hello Elastic Scale tools in order tootake advantage of hello benefits of Elastic jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="decc6-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="decc6-109">Prerequisites</span></span>
<span data-ttu-id="decc6-110">Pobierz i uruchom hello [wprowadzenie próbki narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="decc6-110">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="decc6-111">Tworzenie mapy niezależnego fragmentu manager za pomocą hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="decc6-111">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="decc6-112">W tym miejscu spowoduje utworzenie mapy niezależnego fragmentu manager oraz kilka fragmentów, następuje wstawiania danych do odłamków hello.</span><span class="sxs-lookup"><span data-stu-id="decc6-112">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="decc6-113">Jeśli masz już skonfigurowano w nich danych podzielonej odłamków, można pominąć hello następujące kroki i przenieść toohello następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="decc6-113">If you already have shards set up with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="decc6-114">Tworzenie i uruchamianie hello **wprowadzenie do korzystania z narzędzi elastycznej bazy danych** przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="decc6-114">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="decc6-115">Wykonaj kroki hello aż do kroku 7 w sekcji hello [pobieranie i uruchamianie aplikacji przykładowej hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="decc6-115">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="decc6-116">Na końcu hello kroku 7 zostanie wyświetlony hello następującego wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="decc6-116">At hello end of Step 7, you will see hello following command prompt:</span></span>

   ![Wiersz polecenia](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. <span data-ttu-id="decc6-118">W oknie polecenia hello, wpisz "1", a następnie naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="decc6-118">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="decc6-119">Tworzy menedżera map niezależnego fragmentu hello i dodaje dwa niezależne toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="decc6-119">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="decc6-120">Następnie wpisz "3" i naciśnij klawisz **Enter**; Powtarzaj tę akcję, cztery razy.</span><span class="sxs-lookup"><span data-stu-id="decc6-120">Then type "3" and press **Enter**; repeat this action four times.</span></span> <span data-ttu-id="decc6-121">Wstawia Przykładowe wiersze danych z fragmentów.</span><span class="sxs-lookup"><span data-stu-id="decc6-121">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="decc6-122">Witaj [Azure Portal](https://portal.azure.com) powinny być widoczne trzech nowych baz danych:</span><span class="sxs-lookup"><span data-stu-id="decc6-122">hello [Azure Portal](https://portal.azure.com) should show three new databases:</span></span>

   ![Visual Studio potwierdzenia](./media/sql-database-elastic-query-getting-started/portal.png)

   <span data-ttu-id="decc6-124">W tym momencie utworzymy odzwierciedla wszystkie hello bazy danych na mapie niezależnego fragmentu hello kolekcji niestandardowej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="decc6-124">At this point, we will create a custom database collection that reflects all hello databases in hello shard map.</span></span> <span data-ttu-id="decc6-125">Spowoduje to zezwolić nam toocreate i wykonać zadanie, które Dodaj nową tabelę między fragmentów.</span><span class="sxs-lookup"><span data-stu-id="decc6-125">This will allow us toocreate and execute a job that add a new table across shards.</span></span>

<span data-ttu-id="decc6-126">W tym miejscu będą zazwyczaj utworzymy obiektu docelowego mapy niezależnego fragmentu przy użyciu hello **AzureSqlJobTarget nowy** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="decc6-126">Here we would usually create a shard map target, using hello **New-AzureSqlJobTarget** cmdlet.</span></span> <span data-ttu-id="decc6-127">Hello niezależnego fragmentu Mapa menedżera z bazy danych musi być ustawiona jako docelowej bazy danych, a następnie mapy określonych niezależnych hello jest określony jako element docelowy.</span><span class="sxs-lookup"><span data-stu-id="decc6-127">hello shard map manager database must be set as a database target and then hello specific shard map is specified as a target.</span></span> <span data-ttu-id="decc6-128">Zamiast tego firma Microsoft będzie tooenumerate wszystkich hello baz danych na serwerze hello a Dodaj hello baz danych toohello nowej niestandardowej kolekcji z wyjątkiem hello bazy danych master.</span><span class="sxs-lookup"><span data-stu-id="decc6-128">Instead, we are going tooenumerate all hello databases in hello server and add hello databases toohello new custom collection with hello exception of master database.</span></span>

## <a name="creates-a-custom-collection-and-add-all-databases-in-hello-server-toohello-custom-collection-target-with-hello-exception-of-master"></a><span data-ttu-id="decc6-129">Tworzy kolekcję niestandardową, a następnie dodaj wszystkie bazy danych w lokalizacji docelowej kolekcji niestandardowej toohello serwera hello z wyjątkiem hello wzorca.</span><span class="sxs-lookup"><span data-stu-id="decc6-129">Creates a custom collection and add all databases in hello server toohello custom collection target with hello exception of master.</span></span>
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
## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="decc6-130">Tworzenie skryptu T-SQL do wykonania dla baz danych</span><span class="sxs-lookup"><span data-stu-id="decc6-130">Create a T-SQL Script for execution across databases</span></span>
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

## <a name="create-hello-job-tooexecute-a-script-across-hello-custom-group-of-databases"></a><span data-ttu-id="decc6-131">Utwórz skrypt tooexecute zadania hello między hello niestandardową grupę baz danych</span><span class="sxs-lookup"><span data-stu-id="decc6-131">Create hello job tooexecute a script across hello custom group of databases</span></span>

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-hello-job"></a><span data-ttu-id="decc6-132">Wykonanie zadania hello</span><span class="sxs-lookup"><span data-stu-id="decc6-132">Execute hello job</span></span>
<span data-ttu-id="decc6-133">Hello następującego skryptu programu PowerShell może być używane tooexecute istniejącego zadania:</span><span class="sxs-lookup"><span data-stu-id="decc6-133">hello following PowerShell script can be used tooexecute an existing job:</span></span>

<span data-ttu-id="decc6-134">Aktualizacja hello następującej zmiennej tooreflect hello żądanego zadania nazwa toohave wykonane:</span><span class="sxs-lookup"><span data-stu-id="decc6-134">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="decc6-135">Pobiera stan hello wykonywania pojedyncze zadanie</span><span class="sxs-lookup"><span data-stu-id="decc6-135">Retrieve hello state of a single job execution</span></span>
<span data-ttu-id="decc6-136">Użyj hello sam **Get-AzureSqlJobExecution** polecenia cmdlet z hello **właściwość IncludeChildren** parametru tooview hello stan wykonania zadania podrzędne, czyli hello określonym stanie dla każdego wykonywania zadania w odniesieniu do każdego celem zadania hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="decc6-136">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-hello-state-across-multiple-job-executions"></a><span data-ttu-id="decc6-137">Wyświetlanie stanu hello między wieloma wykonania zadania</span><span class="sxs-lookup"><span data-stu-id="decc6-137">View hello state across multiple job executions</span></span>
<span data-ttu-id="decc6-138">Witaj **Get AzureSqlJobExecution** polecenie cmdlet ma wiele parametrów opcjonalnych, które mogą być używane toodisplay wielu wykonania zadania, filtrowane przez hello podane parametry.</span><span class="sxs-lookup"><span data-stu-id="decc6-138">hello **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="decc6-139">Hello poniżej przedstawiono niektóre hello możliwości toouse Get-AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="decc6-139">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="decc6-140">Pobierz wszystkie aktywne najwyższego poziomu zadanie wykonaniami:</span><span class="sxs-lookup"><span data-stu-id="decc6-140">Retrieve all active top level job executions:</span></span>

   ```
    Get-AzureSqlJobExecution
   ```

<span data-ttu-id="decc6-141">Pobierz wszystkie wykonaniami najwyższego poziomu zadania, w tym wykonaniami nieaktywnego zadania:</span><span class="sxs-lookup"><span data-stu-id="decc6-141">Retrieve all top level job executions, including inactive job executions:</span></span>

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

<span data-ttu-id="decc6-142">Pobierz wszystkie wykonania zadania podrzędne identyfikatora wykonywania podane zadanie wykonaniami nieaktywnego zadania w tym:</span><span class="sxs-lookup"><span data-stu-id="decc6-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

<span data-ttu-id="decc6-143">Pobierz wszystkie wykonania zadania utworzone za pomocą harmonogramu / zadania kombinacji, w tym nieaktywnych zadań:</span><span class="sxs-lookup"><span data-stu-id="decc6-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

<span data-ttu-id="decc6-144">Pobieranie wszystkich zadań przeznaczonych dla określonej niezależnych mapy, w tym nieaktywnych zadań:</span><span class="sxs-lookup"><span data-stu-id="decc6-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="decc6-145">Pobieranie wszystkich zadań przeznaczonych dla określonej kolekcji niestandardowych, łącznie z nieaktywnych zadań:</span><span class="sxs-lookup"><span data-stu-id="decc6-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="decc6-146">Pobrać listy hello zadanie wykonania zadania w ramach wykonania określonego zadania:</span><span class="sxs-lookup"><span data-stu-id="decc6-146">Retrieve hello list of job task executions within a specific job execution:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

<span data-ttu-id="decc6-147">Pobieranie szczegółów wykonywania zadań zadania:</span><span class="sxs-lookup"><span data-stu-id="decc6-147">Retrieve job task execution details:</span></span>

<span data-ttu-id="decc6-148">Witaj następującego skryptu programu PowerShell może być używane tooview hello szczegóły zadania wykonywania zadań, które jest szczególnie przydatne w przypadku debugowania awarii wykonywania.</span><span class="sxs-lookup"><span data-stu-id="decc6-148">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a><span data-ttu-id="decc6-149">Pobrać błędów w ramach zadania wykonania zadania</span><span class="sxs-lookup"><span data-stu-id="decc6-149">Retrieve failures within job task executions</span></span>
<span data-ttu-id="decc6-150">Obiekt JobTaskExecution Hello zawiera właściwość dla cyklu życia zadania hello wraz z właściwością wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="decc6-150">hello JobTaskExecution object includes a property for hello Lifecycle of hello task along with a Message property.</span></span> <span data-ttu-id="decc6-151">Jeżeli wykonanie zadania zadania nie powiodło się, hello cyklu życia właściwość zostanie ustawiona zbyt** i właściwości wiadomości powitania ustawi toohello Wynikowy komunikat o wyjątku i jego stosu.</span><span class="sxs-lookup"><span data-stu-id="decc6-151">If a job task execution failed, hello Lifecycle property will be set too*Failed* and hello Message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="decc6-152">Jeśli zadanie nie powiodło się, jest ważne tooview hello szczegóły zadania, których nie powiodła się dla danego zadania.</span><span class="sxs-lookup"><span data-stu-id="decc6-152">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

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

## <a name="waiting-for-a-job-execution-toocomplete"></a><span data-ttu-id="decc6-153">Oczekiwanie na toocomplete wykonania zadania</span><span class="sxs-lookup"><span data-stu-id="decc6-153">Waiting for a job execution toocomplete</span></span>
<span data-ttu-id="decc6-154">Hello następującego skryptu programu PowerShell może być używane toowait dla toocomplete zadań zadania:</span><span class="sxs-lookup"><span data-stu-id="decc6-154">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="decc6-155">Tworzenie zasad wykonywania niestandardowych</span><span class="sxs-lookup"><span data-stu-id="decc6-155">Create a custom execution policy</span></span>
<span data-ttu-id="decc6-156">Zadania elastyczne bazy danych obsługuje tworzenie zasad wykonywania niestandardowych, które mogą być stosowane podczas uruchamiania zadania.</span><span class="sxs-lookup"><span data-stu-id="decc6-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="decc6-157">Zasady wykonywania obecnie umożliwiają definiowanie:</span><span class="sxs-lookup"><span data-stu-id="decc6-157">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="decc6-158">Name: Identyfikator hello zasad wykonywania.</span><span class="sxs-lookup"><span data-stu-id="decc6-158">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="decc6-159">Limit czasu zadania: Całkowity czas przed zadania zostaną anulowane przez zadania elastyczne bazy danych.</span><span class="sxs-lookup"><span data-stu-id="decc6-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="decc6-160">Interwał ponawiania prób początkowej: Interwał toowait przed ponowną próbą wykonania pierwszej.</span><span class="sxs-lookup"><span data-stu-id="decc6-160">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="decc6-161">Maksymalny interwał ponawiania: Limit toouse interwałów ponów próbę.</span><span class="sxs-lookup"><span data-stu-id="decc6-161">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="decc6-162">Współczynnik wycofywania interwału ponawiania: Współczynnik używany toocalculate hello dalej interwał między ponownymi próbami.</span><span class="sxs-lookup"><span data-stu-id="decc6-162">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="decc6-163">Witaj używana jest następująca formuła: (początkowej interwał ponawiania próby) * Math.Pow — ((interwał wycofywania współczynnik) (liczba prób) - 2).</span><span class="sxs-lookup"><span data-stu-id="decc6-163">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span>
* <span data-ttu-id="decc6-164">Maksymalna liczba prób: hello maksymalna liczba ponawiania prób tooperform w ramach danego zadania.</span><span class="sxs-lookup"><span data-stu-id="decc6-164">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="decc6-165">domyślne zasady wykonywania Hello używa hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="decc6-165">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="decc6-166">Nazwa: Domyślne zasady wykonywania</span><span class="sxs-lookup"><span data-stu-id="decc6-166">Name: Default execution policy</span></span>
* <span data-ttu-id="decc6-167">Limit czasu zadania: 1 tydzień</span><span class="sxs-lookup"><span data-stu-id="decc6-167">Job Timeout: 1 week</span></span>
* <span data-ttu-id="decc6-168">Interwał ponawiania prób początkowej: 100 milisekund</span><span class="sxs-lookup"><span data-stu-id="decc6-168">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="decc6-169">Maksymalny interwał ponawiania: 30 minut</span><span class="sxs-lookup"><span data-stu-id="decc6-169">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="decc6-170">Spróbuj ponownie współczynnik interwał: 2</span><span class="sxs-lookup"><span data-stu-id="decc6-170">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="decc6-171">Maksymalna liczba prób: 2 147 483 647</span><span class="sxs-lookup"><span data-stu-id="decc6-171">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="decc6-172">Tworzenie zasad wykonywania hello potrzeby:</span><span class="sxs-lookup"><span data-stu-id="decc6-172">Create hello desired execution policy:</span></span>

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

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="decc6-173">Aktualizacja zasad wykonywania niestandardowych</span><span class="sxs-lookup"><span data-stu-id="decc6-173">Update a custom execution policy</span></span>
<span data-ttu-id="decc6-174">Aktualizacja hello potrzeby tooupdate zasad wykonywania:</span><span class="sxs-lookup"><span data-stu-id="decc6-174">Update hello desired execution policy tooupdate:</span></span>

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

## <a name="cancel-a-job"></a><span data-ttu-id="decc6-175">Anulowanie zadania</span><span class="sxs-lookup"><span data-stu-id="decc6-175">Cancel a job</span></span>
<span data-ttu-id="decc6-176">Zadania elastyczne bazy danych obsługuje żądania anulowania zadań.</span><span class="sxs-lookup"><span data-stu-id="decc6-176">Elastic Database Jobs supports jobs cancellation requests.</span></span>  <span data-ttu-id="decc6-177">Jeśli zadania elastyczne bazy danych wykryje żądanie anulowania aktualnie wykonywanego zadania, podejmie toostop hello zadania.</span><span class="sxs-lookup"><span data-stu-id="decc6-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="decc6-178">Istnieją dwa różne sposoby, że zadania elastyczne bazy danych można wykonać anulowania:</span><span class="sxs-lookup"><span data-stu-id="decc6-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="decc6-179">Anulowanie aktualnie wykonywanych zadań: wykrycie anulowania aktualnie uruchomionej zadania anulowania będą podejmowane w hello aktualnie wykonywanych aspekt hello zadań.</span><span class="sxs-lookup"><span data-stu-id="decc6-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="decc6-180">Na przykład: w przypadku długo działające kwerendy obecnie wykonywana jest próba anulowania, nastąpi próba toocancel hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="decc6-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="decc6-181">Anulowanie zadań ponownych prób: W przypadku anulowania wykrycia przez wątek kontroli hello przed uruchomieniu zadania do wykonania, hello kontroli wątku będzie uniknąć uruchamiania zadań hello i zadeklarować żądania hello jak anulowane.</span><span class="sxs-lookup"><span data-stu-id="decc6-181">Canceling Task Retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="decc6-182">Jeśli żądanie anulowania zadań dla zadania nadrzędnego, żądanie anulowania hello będą honorowane dla zadania nadrzędnego hello i wszystkich jego zadań podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="decc6-182">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="decc6-183">toosubmit żądanie anulowania, użyj hello **Stop-AzureSqlJobExecution** polecenia cmdlet i zestaw hello **JobExecutionId** parametru.</span><span class="sxs-lookup"><span data-stu-id="decc6-183">toosubmit a cancellation request, use hello **Stop-AzureSqlJobExecution** cmdlet and set hello **JobExecutionId** parameter.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-hello-jobs-history"></a><span data-ttu-id="decc6-184">Usuwanie zadania według nazwy i historii zadań hello</span><span class="sxs-lookup"><span data-stu-id="decc6-184">Delete a job by name and hello job's history</span></span>
<span data-ttu-id="decc6-185">Zadania elastyczne bazy danych obsługuje asynchroniczne usuwania.</span><span class="sxs-lookup"><span data-stu-id="decc6-185">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="decc6-186">Zadanie może być oznaczony do usunięcia, a hello system spowoduje usunięcie hello zadania i jego historii zadań po zakończeniu wszystkich zadań wykonaniami hello zadania.</span><span class="sxs-lookup"><span data-stu-id="decc6-186">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="decc6-187">Witaj systemu nie będzie automatycznie anulowania wykonaniami aktywnego zadania.</span><span class="sxs-lookup"><span data-stu-id="decc6-187">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="decc6-188">Zamiast tego Stop-AzureSqlJobExecution musi być wywołana toocancel wykonaniami aktywnego zadania.</span><span class="sxs-lookup"><span data-stu-id="decc6-188">Instead, Stop-AzureSqlJobExecution must be invoked toocancel active job executions.</span></span>

<span data-ttu-id="decc6-189">Usuwanie zadania tootrigger, użyj hello **AzureSqlJob Usuń** polecenia cmdlet i zestaw hello **JobName** parametru.</span><span class="sxs-lookup"><span data-stu-id="decc6-189">tootrigger job deletion, use hello **Remove-AzureSqlJob** cmdlet and set hello **JobName** parameter.</span></span>

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a><span data-ttu-id="decc6-190">Tworzenie obiektu docelowego w niestandardowej bazie danych</span><span class="sxs-lookup"><span data-stu-id="decc6-190">Create a custom database target</span></span>
<span data-ttu-id="decc6-191">Obiekty docelowe w niestandardowej bazie danych można zdefiniować w zadania elastycznej bazy danych, które mogą być używane do wykonywania bezpośrednio lub dołączania w ramach grupy niestandardowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="decc6-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span></span> <span data-ttu-id="decc6-192">Ponieważ **pule elastyczne** nie są jeszcze bezpośrednio obsługiwane za pośrednictwem hello interfejsów API programu PowerShell, należy po prostu utworzyć obiekt docelowy w niestandardowej bazie danych oraz miejsca docelowego do kolekcji niestandardowej bazy danych, które obejmuje wszystkie hello bazy danych w puli hello.</span><span class="sxs-lookup"><span data-stu-id="decc6-192">Since **elastic pools** are not yet directly supported via hello PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="decc6-193">Ustaw hello następujące zmienne tooreflect hello potrzeby bazy danych:</span><span class="sxs-lookup"><span data-stu-id="decc6-193">Set hello following variables tooreflect hello desired database information:</span></span>

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a><span data-ttu-id="decc6-194">Utwórz docelowy kolekcji niestandardowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="decc6-194">Create a custom database collection target</span></span>
<span data-ttu-id="decc6-195">Docelowy kolekcji niestandardowej bazy danych może być wykonanie tooenable zdefiniowanych przez wiele obiektów docelowych określonych bazy danych.</span><span class="sxs-lookup"><span data-stu-id="decc6-195">A custom database collection target can be defined tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="decc6-196">Po utworzeniu grupy bazy danych, baz danych może być skojarzony toohello docelowej kolekcji niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="decc6-196">After a database group is created, databases can be associated toohello custom collection target.</span></span>

<span data-ttu-id="decc6-197">Ustaw powitania po konfiguracji docelowej żądanej kolekcji niestandardowych zmiennych tooreflect hello:</span><span class="sxs-lookup"><span data-stu-id="decc6-197">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="decc6-198">Dodawanie baz danych tooa w niestandardowej bazie danych kolekcji docelowego</span><span class="sxs-lookup"><span data-stu-id="decc6-198">Add databases tooa custom database collection target</span></span>
<span data-ttu-id="decc6-199">Obiekty docelowe bazy danych może być skojarzony z niestandardowej bazie danych kolekcji elementów docelowych toocreate grupę baz danych.</span><span class="sxs-lookup"><span data-stu-id="decc6-199">Database targets can be associated with custom database collection targets toocreate a group of databases.</span></span> <span data-ttu-id="decc6-200">Zawsze, gdy tworzone jest zadanie cel kolekcji niestandardowej bazy danych, będzie tootarget rozwinięte hello bazy danych skojarzony toohello grupy w momencie hello wykonywania.</span><span class="sxs-lookup"><span data-stu-id="decc6-200">Whenever a job is created that targets a custom database collection target, it will be expanded tootarget hello databases associated toohello group at hello time of execution.</span></span>

<span data-ttu-id="decc6-201">Dodaj określonej kolekcji niestandardowych hello potrzeby bazy danych tooa:</span><span class="sxs-lookup"><span data-stu-id="decc6-201">Add hello desired database tooa specific custom collection:</span></span>

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="decc6-202">Przejrzyj hello bazy danych, w docelowej kolekcji niestandardowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="decc6-202">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="decc6-203">Użyj hello **Get-AzureSqlJobTarget** polecenia cmdlet tooretrieve hello podrzędnej bazy danych, w docelowej kolekcji niestandardowej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="decc6-203">Use hello **Get-AzureSqlJobTarget** cmdlet tooretrieve hello child databases within a custom database collection target.</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="decc6-204">Utwórz skrypt tooexecute zadania w docelowej kolekcji niestandardowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="decc6-204">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="decc6-205">Użyj hello **AzureSqlJob nowy** toocreate polecenia cmdlet zadania przed grupę baz danych, wynika z docelowej kolekcji niestandardowej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="decc6-205">Use hello **New-AzureSqlJob** cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="decc6-206">Zadania elastyczne bazy danych będzie rozszerzać hello zadania do wielu zadań podrzędnych każdego odpowiednia baza danych tooa skojarzone z hello w niestandardowej bazie danych kolekcji docelowych i upewnij się, że hello skrypt zostanie wykonany w każdej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="decc6-206">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="decc6-207">Ponownie ważne jest, że skrypty są odporne tooretries toobe idempotentności.</span><span class="sxs-lookup"><span data-stu-id="decc6-207">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a><span data-ttu-id="decc6-208">Zbieranie danych dla baz danych</span><span class="sxs-lookup"><span data-stu-id="decc6-208">Data collection across databases</span></span>
<span data-ttu-id="decc6-209">**Zadania elastyczne bazy danych** obsługuje wykonywanie zapytania na grupę baz danych i wysyła hello wyniki tooa określonej tabeli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="decc6-209">**Elastic Database jobs** supports executing a query across a group of databases and sends hello results tooa specified database’s table.</span></span> <span data-ttu-id="decc6-210">Witaj tabeli może być badana po hello fakt toosee hello wyniki zapytania w każdej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="decc6-210">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="decc6-211">Zapewnia to tooexecute asynchronicznego mechanizmu zapytania przez wiele baz danych.</span><span class="sxs-lookup"><span data-stu-id="decc6-211">This provides an asynchronous mechanism tooexecute a query across many databases.</span></span> <span data-ttu-id="decc6-212">Błąd przypadkach, takich jak jednej z baz danych hello są tymczasowo niedostępne są obsługiwane automatycznie za pośrednictwem ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="decc6-212">Failure cases such as one of hello databases being temporarily unavailable are handled automatically via retries.</span></span>

<span data-ttu-id="decc6-213">Witaj określonej lokalizacji docelowej tabeli będą tworzone automatycznie, jeśli jeszcze nie istnieje, zgodnego schematu hello hello zwrócił zestaw wyników.</span><span class="sxs-lookup"><span data-stu-id="decc6-213">hello specified destination table will be automatically created if it does not yet exist, matching hello schema of hello returned result set.</span></span> <span data-ttu-id="decc6-214">Jeśli wykonanie skrypt zwraca wiele zestawów wyników, zadania elastycznej bazy danych wysyła hello pierwszy toohello co podane tabeli docelowej.</span><span class="sxs-lookup"><span data-stu-id="decc6-214">If a script execution returns multiple result sets, Elastic Database jobs will only send hello first one toohello provided destination table.</span></span>

<span data-ttu-id="decc6-215">Witaj następującego skryptu programu PowerShell może być używane tooexecute skrypt zbieranie jej wyników do określonej tabeli.</span><span class="sxs-lookup"><span data-stu-id="decc6-215">hello following PowerShell script can be used tooexecute a script collecting its results into a specified table.</span></span> <span data-ttu-id="decc6-216">Ten skrypt założono, że utworzono skryptu T-SQL, który generuje pojedynczy zestaw wyników i docelowej kolekcji niestandardowej bazie danych została utworzona.</span><span class="sxs-lookup"><span data-stu-id="decc6-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span></span>

<span data-ttu-id="decc6-217">Ustaw powitania po tooreflect skryptu hello potrzeby, poświadczenia i wykonywania obiekt docelowy:</span><span class="sxs-lookup"><span data-stu-id="decc6-217">Set hello following tooreflect hello desired script, credentials, and execution target:</span></span>

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

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="decc6-218">Tworzenie i uruchamianie zadania dla scenariuszy zbierania danych</span><span class="sxs-lookup"><span data-stu-id="decc6-218">Create and start a job for data collection scenarios</span></span>
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a><span data-ttu-id="decc6-219">Utwórz harmonogram wykonywania zadania przy użyciu wyzwalacz zadania</span><span class="sxs-lookup"><span data-stu-id="decc6-219">Create a schedule for job execution using a job trigger</span></span>
<span data-ttu-id="decc6-220">Witaj następującego skryptu programu PowerShell może być używane toocreate reoccurring harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="decc6-220">hello following PowerShell script can be used toocreate a reoccurring schedule.</span></span> <span data-ttu-id="decc6-221">Ten skrypt używa interwał jedną minutę, ale nowy AzureSqlJobSchedule obsługuje również parametry - DayInterval, - HourInterval i - MonthInterval, - WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="decc6-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="decc6-222">Można utworzyć harmonogramy, które są wykonywane tylko raz przekazywanie przez - jednorazowe.</span><span class="sxs-lookup"><span data-stu-id="decc6-222">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="decc6-223">Utwórz nowy harmonogram:</span><span class="sxs-lookup"><span data-stu-id="decc6-223">Create a new schedule:</span></span>
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-toohave-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="decc6-224">Utwórz zadanie wykonywane zgodnie z harmonogramem czasu toohave wyzwalacz zadania</span><span class="sxs-lookup"><span data-stu-id="decc6-224">Create a job trigger toohave a job executed on a time schedule</span></span>
<span data-ttu-id="decc6-225">Wyzwalacz zadania mogą być zdefiniowane toohave zgodnie z zadania wykonywane harmonogram tooa.</span><span class="sxs-lookup"><span data-stu-id="decc6-225">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="decc6-226">Witaj następującego skryptu programu PowerShell może być używane toocreate wyzwalacza zadania.</span><span class="sxs-lookup"><span data-stu-id="decc6-226">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="decc6-227">Ustaw hello następujące zmienne toocorrespond toohello żądanego zadania i harmonogramu:</span><span class="sxs-lookup"><span data-stu-id="decc6-227">Set hello following variables toocorrespond toohello desired job and schedule:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="decc6-228">Usuń skojarzenie zaplanowane zadanie toostop wykonywanie zgodnie z harmonogramem</span><span class="sxs-lookup"><span data-stu-id="decc6-228">Remove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="decc6-229">można usunąć toodiscontinue pojawiał wykonywania zadań za pomocą wyzwalacza zadania hello wyzwalacza zadania.</span><span class="sxs-lookup"><span data-stu-id="decc6-229">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span>
<span data-ttu-id="decc6-230">Usuwanie zadania toostop wyzwalacz zadania wykonywane zgodnie z harmonogramem tooa przy użyciu hello **AzureSqlJobTrigger Usuń** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="decc6-230">Remove a job trigger toostop a job from being executed according tooa schedule using hello **Remove-AzureSqlJobTrigger** cmdlet.</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="decc6-231">Importuj tooExcel wyników zapytania elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="decc6-231">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="decc6-232">Możesz zaimportować hello wyników z pliku programu Excel tooan zapytania.</span><span class="sxs-lookup"><span data-stu-id="decc6-232">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="decc6-233">Uruchom program Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="decc6-233">Launch Excel 2013.</span></span>
2. <span data-ttu-id="decc6-234">Przejdź toohello **danych** wstążki.</span><span class="sxs-lookup"><span data-stu-id="decc6-234">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="decc6-235">Kliknij przycisk **z innych źródeł** i kliknij przycisk **z programu SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="decc6-235">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Importowania z programu Excel z innych źródeł](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. <span data-ttu-id="decc6-237">W hello **Kreator połączenia danych** wpisz powitania serwera nazwę i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="decc6-237">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="decc6-238">Następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="decc6-238">Then click **Next**.</span></span>
5. <span data-ttu-id="decc6-239">W oknie dialogowym hello **hello wybierz bazy danych, która zawiera dane hello**, wybierz pozycję hello **ElasticDBQuery** bazy danych.</span><span class="sxs-lookup"><span data-stu-id="decc6-239">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="decc6-240">Wybierz hello **klientów** tabeli w widoku listy hello, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="decc6-240">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="decc6-241">Następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="decc6-241">Then click **Finish**.</span></span>
7. <span data-ttu-id="decc6-242">W hello **i zaimportuj dane** formularza, w obszarze **wybierz sposób tooview tych danych w skoroszycie**, wybierz pozycję **tabeli** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="decc6-242">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="decc6-243">Witaj wszystkie wiersze z **klientów** tabeli, przechowywane w różnych odłamków wypełnić hello arkuszu programu Excel.</span><span class="sxs-lookup"><span data-stu-id="decc6-243">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="decc6-244">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="decc6-244">Next steps</span></span>
<span data-ttu-id="decc6-245">Możesz teraz użyć funkcji danych programu Excel.</span><span class="sxs-lookup"><span data-stu-id="decc6-245">You can now use Excel’s data functions.</span></span> <span data-ttu-id="decc6-246">Użyj parametrów połączenia hello nazwę serwera, nazwa bazy danych i poświadczeń tooconnect BI i dane integracji narzędzia toohello zapytania elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="decc6-246">Use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="decc6-247">Upewnij się, czy program SQL Server jest obsługiwana jako źródło danych dla własnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="decc6-247">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="decc6-248">Znajdują się toohello elastycznej zapytanie do bazy danych i tabele zewnętrzne, podobnie jak wszystkie inne bazy danych programu SQL Server i czy można połączyć toowith własnych narzędzi tabel programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="decc6-248">Refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="decc6-249">Koszty</span><span class="sxs-lookup"><span data-stu-id="decc6-249">Cost</span></span>
<span data-ttu-id="decc6-250">Brak bez dodatkowych opłat dla funkcji zapytania hello elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="decc6-250">There is no additional charge for using hello Elastic Database query feature.</span></span> <span data-ttu-id="decc6-251">Jednak w tej chwili ta funkcja jest dostępna tylko w bazach danych premium jako punkt końcowy, ale odłamków hello może być dowolnym warstwy usługi.</span><span class="sxs-lookup"><span data-stu-id="decc6-251">However, at this time this feature is available only on premium databases as an end point, but hello shards can be of any service tier.</span></span>

<span data-ttu-id="decc6-252">Aby uzyskać informacje o cenach zobacz [szczegóły cennika bazy danych SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="decc6-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
