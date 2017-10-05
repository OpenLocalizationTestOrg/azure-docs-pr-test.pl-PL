---
title: Wprowadzenie zadania elastycznej bazy danych | Dokumentacja firmy Microsoft
description: "jak używać zadania elastycznej bazy danych"
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
ms.openlocfilehash: 05c20e880d4eb1eacdecc0c4c7e7491dfe1e6a89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-elastic-database-jobs"></a><span data-ttu-id="f051d-103">Wprowadzenie zadania elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="f051d-103">Getting started with Elastic Database jobs</span></span>
<span data-ttu-id="f051d-104">Baza danych zadania elastyczne (wersja zapoznawcza) w bazie danych SQL Azure pozwala na niezawodność wykonywanie skryptów T-SQL, obejmującej wiele baz danych podczas Automatyczne ponawianie próby i zapewnienia gwarancji ostatecznego zakończenia.</span><span class="sxs-lookup"><span data-stu-id="f051d-104">Elastic Database jobs (preview) for Azure SQL Database allows you to reliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span></span> <span data-ttu-id="f051d-105">Aby uzyskać więcej informacji na temat funkcji zadania elastycznej bazy danych, zobacz [strony Przegląd funkcji](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f051d-105">For more information about the Elastic Database job feature, please see the [feature overview page](sql-database-elastic-jobs-overview.md).</span></span>

<span data-ttu-id="f051d-106">W tym temacie rozszerza próbki w [wprowadzenie do korzystania z narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f051d-106">This topic extends the sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span> <span data-ttu-id="f051d-107">Po zakończeniu zostanie: Dowiedz się, jak utworzyć i zarządzać zadaniami, które zarządzają grupy powiązanych baz danych.</span><span class="sxs-lookup"><span data-stu-id="f051d-107">When completed, you will: learn how to create and manage jobs that manage a group of related databases.</span></span> <span data-ttu-id="f051d-108">Nie jest to wymagane, aby można było skorzystać z zalet elastycznej zadań za pomocą narzędzi elastycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="f051d-108">It is not required to use the Elastic Scale tools in order to take advantage of the benefits of Elastic jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f051d-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f051d-109">Prerequisites</span></span>
<span data-ttu-id="f051d-110">Pobierz i uruchom [wprowadzenie próbki narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f051d-110">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-the-sample-app"></a><span data-ttu-id="f051d-111">Utwórz identyfikator niezależnego fragmentu mapy manager za pomocą przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="f051d-111">Create a shard map manager using the sample app</span></span>
<span data-ttu-id="f051d-112">W tym polu spowoduje utworzenie mapy niezależnego fragmentu manager oraz kilka fragmentów, następuje wstawiania danych do fragmentów.</span><span class="sxs-lookup"><span data-stu-id="f051d-112">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span></span> <span data-ttu-id="f051d-113">Jeśli masz już skonfigurowano w nich danych podzielonej odłamków, możesz pominąć następujące kroki i przejść do następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="f051d-113">If you already have shards set up with sharded data in them, you can skip the following steps and move to the next section.</span></span>

1. <span data-ttu-id="f051d-114">Tworzenie i uruchamianie **wprowadzenie do korzystania z narzędzi elastycznej bazy danych** przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f051d-114">Build and run the **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="f051d-115">Postępuj zgodnie z instrukcjami aż do kroku 7 w sekcji [pobieranie i uruchamianie aplikacji przykładowej](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="f051d-115">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="f051d-116">Po zakończeniu kroku 7 zostanie wyświetlony następujący wiersz polecenia:</span><span class="sxs-lookup"><span data-stu-id="f051d-116">At the end of Step 7, you will see the following command prompt:</span></span>

   ![Wiersz polecenia](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. <span data-ttu-id="f051d-118">W oknie wiersza polecenia wpisz "1" i naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="f051d-118">In the command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="f051d-119">Tworzy identyfikator niezależnego fragmentu menedżera map i dodaje dwa niezależne do serwera.</span><span class="sxs-lookup"><span data-stu-id="f051d-119">This creates the shard map manager, and adds two shards to the server.</span></span> <span data-ttu-id="f051d-120">Następnie wpisz "3" i naciśnij klawisz **Enter**; Powtarzaj tę akcję, cztery razy.</span><span class="sxs-lookup"><span data-stu-id="f051d-120">Then type "3" and press **Enter**; repeat this action four times.</span></span> <span data-ttu-id="f051d-121">Wstawia Przykładowe wiersze danych z fragmentów.</span><span class="sxs-lookup"><span data-stu-id="f051d-121">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="f051d-122">[Azure Portal](https://portal.azure.com) powinny być widoczne trzech nowych baz danych:</span><span class="sxs-lookup"><span data-stu-id="f051d-122">The [Azure Portal](https://portal.azure.com) should show three new databases:</span></span>

   ![Visual Studio potwierdzenia](./media/sql-database-elastic-query-getting-started/portal.png)

   <span data-ttu-id="f051d-124">W tym momencie utworzymy kolekcji niestandardowej bazy danych, które odzwierciedla wszystkie bazy danych na mapie niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="f051d-124">At this point, we will create a custom database collection that reflects all the databases in the shard map.</span></span> <span data-ttu-id="f051d-125">Pozwoli to nam na tworzenie i wykonywanie zadanie, które Dodaj nową tabelę między fragmentów.</span><span class="sxs-lookup"><span data-stu-id="f051d-125">This will allow us to create and execute a job that add a new table across shards.</span></span>

<span data-ttu-id="f051d-126">W tym miejscu będą zazwyczaj utworzymy mapy niezależnego fragmentu docelowych przy użyciu **AzureSqlJobTarget nowy** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f051d-126">Here we would usually create a shard map target, using the **New-AzureSqlJobTarget** cmdlet.</span></span> <span data-ttu-id="f051d-127">Bazy danych Menedżera mapy niezależnego fragmentu musi być ustawiona jako docelowej bazy danych, a następnie mapy określonych niezależnego fragmentu jest określony jako element docelowy.</span><span class="sxs-lookup"><span data-stu-id="f051d-127">The shard map manager database must be set as a database target and then the specific shard map is specified as a target.</span></span> <span data-ttu-id="f051d-128">Zamierzamy wylicza wszystkie bazy danych na serwerze i dodać bazy danych do nowej kolekcji niestandardowych z wyjątkiem bazy danych master.</span><span class="sxs-lookup"><span data-stu-id="f051d-128">Instead, we are going to enumerate all the databases in the server and add the databases to the new custom collection with the exception of master database.</span></span>

## <a name="creates-a-custom-collection-and-add-all-databases-in-the-server-to-the-custom-collection-target-with-the-exception-of-master"></a><span data-ttu-id="f051d-129">Utworzenie kolekcji niestandardowych i dodać wszystkie bazy danych na serwerze docelowym kolekcji niestandardowych z wyjątkiem wzorca.</span><span class="sxs-lookup"><span data-stu-id="f051d-129">Creates a custom collection and add all databases in the server to the custom collection target with the exception of master.</span></span>
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
             Write-Host $currentdb "is already in the custom collection target" $CustomCollectionName"."
        }

        else
        {
            throw $_
        }
    }
    $ErrorActionPreference = "Continue"
   }
   ```
## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="f051d-130">Tworzenie skryptu T-SQL do wykonania dla baz danych</span><span class="sxs-lookup"><span data-stu-id="f051d-130">Create a T-SQL Script for execution across databases</span></span>
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

## <a name="create-the-job-to-execute-a-script-across-the-custom-group-of-databases"></a><span data-ttu-id="f051d-131">Utwórz zadanie można wykonać skryptu na niestandardową grupę baz danych</span><span class="sxs-lookup"><span data-stu-id="f051d-131">Create the job to execute a script across the custom group of databases</span></span>

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-the-job"></a><span data-ttu-id="f051d-132">Wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="f051d-132">Execute the job</span></span>
<span data-ttu-id="f051d-133">Poniższy skrypt programu PowerShell może służyć do wykonywania istniejącego zadania:</span><span class="sxs-lookup"><span data-stu-id="f051d-133">The following PowerShell script can be used to execute an existing job:</span></span>

<span data-ttu-id="f051d-134">Aktualizacja następującej zmiennej w celu odzwierciedlenia nazwa żądanego zadania zostały wykonane:</span><span class="sxs-lookup"><span data-stu-id="f051d-134">Update the following variable to reflect the desired job name to have executed:</span></span>

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-the-state-of-a-single-job-execution"></a><span data-ttu-id="f051d-135">Pobiera stan wykonywania pojedyncze zadanie</span><span class="sxs-lookup"><span data-stu-id="f051d-135">Retrieve the state of a single job execution</span></span>
<span data-ttu-id="f051d-136">Używać tego samego **Get-AzureSqlJobExecution** polecenia cmdlet z **właściwość IncludeChildren** parametr, aby wyświetlić stan wykonania zadania podrzędne, czyli określonym stanie dla każdego wykonywania zadania dla każdej bazy danych Celem tego zadania.</span><span class="sxs-lookup"><span data-stu-id="f051d-136">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-the-state-across-multiple-job-executions"></a><span data-ttu-id="f051d-137">Wyświetl stan całej wielu wykonania zadania</span><span class="sxs-lookup"><span data-stu-id="f051d-137">View the state across multiple job executions</span></span>
<span data-ttu-id="f051d-138">**Get AzureSqlJobExecution** polecenie cmdlet ma wiele parametry opcjonalne, które mogą służyć do wyświetlania wielu wykonania zadania, filtrować za pomocą podanych parametrów.</span><span class="sxs-lookup"><span data-stu-id="f051d-138">The **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span></span> <span data-ttu-id="f051d-139">Poniżej przedstawiono niektóre możliwe sposoby używania Get-AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="f051d-139">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="f051d-140">Pobierz wszystkie aktywne najwyższego poziomu zadanie wykonaniami:</span><span class="sxs-lookup"><span data-stu-id="f051d-140">Retrieve all active top level job executions:</span></span>

   ```
    Get-AzureSqlJobExecution
   ```

<span data-ttu-id="f051d-141">Pobierz wszystkie wykonaniami najwyższego poziomu zadania, w tym wykonaniami nieaktywnego zadania:</span><span class="sxs-lookup"><span data-stu-id="f051d-141">Retrieve all top level job executions, including inactive job executions:</span></span>

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

<span data-ttu-id="f051d-142">Pobierz wszystkie wykonania zadania podrzędne identyfikatora wykonywania podane zadanie wykonaniami nieaktywnego zadania w tym:</span><span class="sxs-lookup"><span data-stu-id="f051d-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

<span data-ttu-id="f051d-143">Pobierz wszystkie wykonania zadania utworzone za pomocą harmonogramu / zadania kombinacji, w tym nieaktywnych zadań:</span><span class="sxs-lookup"><span data-stu-id="f051d-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

<span data-ttu-id="f051d-144">Pobieranie wszystkich zadań przeznaczonych dla określonej niezależnych mapy, w tym nieaktywnych zadań:</span><span class="sxs-lookup"><span data-stu-id="f051d-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="f051d-145">Pobieranie wszystkich zadań przeznaczonych dla określonej kolekcji niestandardowych, łącznie z nieaktywnych zadań:</span><span class="sxs-lookup"><span data-stu-id="f051d-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="f051d-146">Pobieranie listy zadanie wykonania zadania w ramach wykonania określonego zadania:</span><span class="sxs-lookup"><span data-stu-id="f051d-146">Retrieve the list of job task executions within a specific job execution:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

<span data-ttu-id="f051d-147">Pobieranie szczegółów wykonywania zadań zadania:</span><span class="sxs-lookup"><span data-stu-id="f051d-147">Retrieve job task execution details:</span></span>

<span data-ttu-id="f051d-148">Poniższy skrypt programu PowerShell może służyć do wyświetlania szczegółów zadania wykonywania zadania, które jest szczególnie przydatne w przypadku debugowania awarii wykonywania.</span><span class="sxs-lookup"><span data-stu-id="f051d-148">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span></span>
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a><span data-ttu-id="f051d-149">Pobrać błędów w ramach zadania wykonania zadania</span><span class="sxs-lookup"><span data-stu-id="f051d-149">Retrieve failures within job task executions</span></span>
<span data-ttu-id="f051d-150">Obiekt JobTaskExecution zawiera właściwość dla cyklu życia zadania wraz z właściwością wiadomości.</span><span class="sxs-lookup"><span data-stu-id="f051d-150">The JobTaskExecution object includes a property for the Lifecycle of the task along with a Message property.</span></span> <span data-ttu-id="f051d-151">Jeżeli wykonanie zadania zadania nie powiodło się, zostanie ustawiona właściwość cyklu życia do ** i będzie można ustawić właściwości wiadomości Wynikowy komunikat o wyjątku i jego stosu.</span><span class="sxs-lookup"><span data-stu-id="f051d-151">If a job task execution failed, the Lifecycle property will be set to *Failed* and the Message property will be set to the resulting exception message and its stack.</span></span> <span data-ttu-id="f051d-152">Jeśli zadanie nie powiodło się, jest ważne wyświetlić szczegóły zadania, których nie powiodła się dla danego zadania.</span><span class="sxs-lookup"><span data-stu-id="f051d-152">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span></span>

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

## <a name="waiting-for-a-job-execution-to-complete"></a><span data-ttu-id="f051d-153">Oczekiwanie na ukończenie wykonywania zadania</span><span class="sxs-lookup"><span data-stu-id="f051d-153">Waiting for a job execution to complete</span></span>
<span data-ttu-id="f051d-154">Poniższy skrypt programu PowerShell można czekać na ukończenie zadania zadania:</span><span class="sxs-lookup"><span data-stu-id="f051d-154">The following PowerShell script can be used to wait for a job task to complete:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="f051d-155">Tworzenie zasad wykonywania niestandardowych</span><span class="sxs-lookup"><span data-stu-id="f051d-155">Create a custom execution policy</span></span>
<span data-ttu-id="f051d-156">Zadania elastyczne bazy danych obsługuje tworzenie zasad wykonywania niestandardowych, które mogą być stosowane podczas uruchamiania zadania.</span><span class="sxs-lookup"><span data-stu-id="f051d-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="f051d-157">Zasady wykonywania obecnie umożliwiają definiowanie:</span><span class="sxs-lookup"><span data-stu-id="f051d-157">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="f051d-158">Nazwa: Identyfikator zasad wykonywania.</span><span class="sxs-lookup"><span data-stu-id="f051d-158">Name: Identifier for the execution policy.</span></span>
* <span data-ttu-id="f051d-159">Limit czasu zadania: Całkowity czas przed zadania zostaną anulowane przez zadania elastyczne bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f051d-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="f051d-160">Początkowa interwału ponawiania prób: Interwał oczekiwania przed pierwszym ponów próbę.</span><span class="sxs-lookup"><span data-stu-id="f051d-160">Initial Retry Interval: Interval to wait before first retry.</span></span>
* <span data-ttu-id="f051d-161">Maksymalny interwał ponawiania: Zakończenia interwałów ponawiania do użycia.</span><span class="sxs-lookup"><span data-stu-id="f051d-161">Maximum Retry Interval: Cap of retry intervals to use.</span></span>
* <span data-ttu-id="f051d-162">Ponów próbę współczynnik wycofywania interwał: Współczynnik używane do obliczania następnego interwał między ponownymi próbami.</span><span class="sxs-lookup"><span data-stu-id="f051d-162">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span></span>  <span data-ttu-id="f051d-163">Używana jest następująca formuła: (początkowej interwał ponawiania próby) * Math.Pow — ((interwał wycofywania współczynnik) (liczba prób) - 2).</span><span class="sxs-lookup"><span data-stu-id="f051d-163">The following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span>
* <span data-ttu-id="f051d-164">Maksymalna liczba prób: Maksymalną liczbę ponownych prób do wykonania w ramach danego zadania.</span><span class="sxs-lookup"><span data-stu-id="f051d-164">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span></span>

<span data-ttu-id="f051d-165">Domyślne zasady wykonywania korzysta z następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="f051d-165">The default execution policy uses the following values:</span></span>

* <span data-ttu-id="f051d-166">Nazwa: Domyślne zasady wykonywania</span><span class="sxs-lookup"><span data-stu-id="f051d-166">Name: Default execution policy</span></span>
* <span data-ttu-id="f051d-167">Limit czasu zadania: 1 tydzień</span><span class="sxs-lookup"><span data-stu-id="f051d-167">Job Timeout: 1 week</span></span>
* <span data-ttu-id="f051d-168">Interwał ponawiania prób początkowej: 100 milisekund</span><span class="sxs-lookup"><span data-stu-id="f051d-168">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="f051d-169">Maksymalny interwał ponawiania: 30 minut</span><span class="sxs-lookup"><span data-stu-id="f051d-169">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="f051d-170">Spróbuj ponownie współczynnik interwał: 2</span><span class="sxs-lookup"><span data-stu-id="f051d-170">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="f051d-171">Maksymalna liczba prób: 2 147 483 647</span><span class="sxs-lookup"><span data-stu-id="f051d-171">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="f051d-172">Tworzenie zasad wykonywania żądanego:</span><span class="sxs-lookup"><span data-stu-id="f051d-172">Create the desired execution policy:</span></span>

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

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="f051d-173">Aktualizacja zasad wykonywania niestandardowych</span><span class="sxs-lookup"><span data-stu-id="f051d-173">Update a custom execution policy</span></span>
<span data-ttu-id="f051d-174">Aktualizacja zasad wykonywania żądanej aktualizacji:</span><span class="sxs-lookup"><span data-stu-id="f051d-174">Update the desired execution policy to update:</span></span>

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

## <a name="cancel-a-job"></a><span data-ttu-id="f051d-175">Anulowanie zadania</span><span class="sxs-lookup"><span data-stu-id="f051d-175">Cancel a job</span></span>
<span data-ttu-id="f051d-176">Zadania elastyczne bazy danych obsługuje żądania anulowania zadań.</span><span class="sxs-lookup"><span data-stu-id="f051d-176">Elastic Database Jobs supports jobs cancellation requests.</span></span>  <span data-ttu-id="f051d-177">Jeśli zadania elastyczne bazy danych wykryje żądanie anulowania aktualnie wykonywanego zadania, spróbuje zatrzymać zadanie.</span><span class="sxs-lookup"><span data-stu-id="f051d-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span></span>

<span data-ttu-id="f051d-178">Istnieją dwa różne sposoby, że zadania elastyczne bazy danych można wykonać anulowania:</span><span class="sxs-lookup"><span data-stu-id="f051d-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="f051d-179">Anulowanie aktualnie wykonywanych zadań: wykrycie anulowania aktualnie uruchomionej zadania anulowania będą podejmowane w aspekcie aktualnie wykonywanego zadania.</span><span class="sxs-lookup"><span data-stu-id="f051d-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span></span>  <span data-ttu-id="f051d-180">Na przykład: w przypadku długo działające kwerendy obecnie wykonywana jest próba anulowania, nastąpi próba anulować wykonywanie zapytania.</span><span class="sxs-lookup"><span data-stu-id="f051d-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span></span>
2. <span data-ttu-id="f051d-181">Anulowanie zadań ponownych prób: W przypadku anulowania wykrycia przez wątek kontroli przed uruchomieniu zadania do wykonania, wątku kontroli będzie uniknąć uruchamiania zadania i zadeklarować żądania, jak anulowane.</span><span class="sxs-lookup"><span data-stu-id="f051d-181">Canceling Task Retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span></span>

<span data-ttu-id="f051d-182">Jeśli żądanie anulowania zadań dla zadania nadrzędnego, żądanie anulowania będą honorowane dla zadania nadrzędnego i wszystkich jego zadań podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="f051d-182">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span></span>

<span data-ttu-id="f051d-183">Aby przesłać żądanie anulowania, użyj **Stop-AzureSqlJobExecution** polecenia cmdlet i ustaw **JobExecutionId** parametru.</span><span class="sxs-lookup"><span data-stu-id="f051d-183">To submit a cancellation request, use the **Stop-AzureSqlJobExecution** cmdlet and set the **JobExecutionId** parameter.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-the-jobs-history"></a><span data-ttu-id="f051d-184">Usuwanie zadania według nazwy i historii zadań</span><span class="sxs-lookup"><span data-stu-id="f051d-184">Delete a job by name and the job's history</span></span>
<span data-ttu-id="f051d-185">Zadania elastyczne bazy danych obsługuje asynchroniczne usuwania.</span><span class="sxs-lookup"><span data-stu-id="f051d-185">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="f051d-186">Zadanie może być oznaczony do usunięcia, a system spowoduje usunięcie zadania i jego historii zadań po zakończeniu wszystkich wykonania zadań dla zadania.</span><span class="sxs-lookup"><span data-stu-id="f051d-186">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span></span> <span data-ttu-id="f051d-187">System nie zostanie automatycznie anulowania wykonaniami aktywnego zadania.</span><span class="sxs-lookup"><span data-stu-id="f051d-187">The system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="f051d-188">Zamiast tego Stop-AzureSqlJobExecution muszą być wywoływane anulować wykonaniami aktywnego zadania.</span><span class="sxs-lookup"><span data-stu-id="f051d-188">Instead, Stop-AzureSqlJobExecution must be invoked to cancel active job executions.</span></span>

<span data-ttu-id="f051d-189">Aby wyzwolić usunięcia zadania, należy użyć **AzureSqlJob Usuń** polecenia cmdlet i ustaw **JobName** parametru.</span><span class="sxs-lookup"><span data-stu-id="f051d-189">To trigger job deletion, use the **Remove-AzureSqlJob** cmdlet and set the **JobName** parameter.</span></span>

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a><span data-ttu-id="f051d-190">Tworzenie obiektu docelowego w niestandardowej bazie danych</span><span class="sxs-lookup"><span data-stu-id="f051d-190">Create a custom database target</span></span>
<span data-ttu-id="f051d-191">Obiekty docelowe w niestandardowej bazie danych można zdefiniować w zadania elastycznej bazy danych, które mogą być używane do wykonywania bezpośrednio lub dołączania w ramach grupy niestandardowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f051d-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span></span> <span data-ttu-id="f051d-192">Ponieważ **pule elastyczne** nie są jeszcze bezpośrednio obsługiwane za pośrednictwem interfejsów API środowiska PowerShell, możesz po prostu utworzyć obiekt docelowy w niestandardowej bazie danych oraz miejsca docelowego do kolekcji niestandardowej bazy danych, które obejmuje wszystkie bazy danych w puli.</span><span class="sxs-lookup"><span data-stu-id="f051d-192">Since **elastic pools** are not yet directly supported via the PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all the databases in the pool.</span></span>

<span data-ttu-id="f051d-193">Ustaw następujące zmienne, aby odzwierciedlić informacje o żądanej bazy danych:</span><span class="sxs-lookup"><span data-stu-id="f051d-193">Set the following variables to reflect the desired database information:</span></span>

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a><span data-ttu-id="f051d-194">Utwórz docelowy kolekcji niestandardowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="f051d-194">Create a custom database collection target</span></span>
<span data-ttu-id="f051d-195">Umożliwia wykonanie przez wiele obiektów docelowych określonych bazy danych można zdefiniować docelowej kolekcji niestandardowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f051d-195">A custom database collection target can be defined to enable execution across multiple defined database targets.</span></span> <span data-ttu-id="f051d-196">Po utworzeniu grupy bazy danych, bazy danych może być skojarzony z docelowym kolekcji niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="f051d-196">After a database group is created, databases can be associated to the custom collection target.</span></span>

<span data-ttu-id="f051d-197">Ustaw następujące zmienne w celu uwzględnienia konfiguracji docelowej żądanej kolekcji niestandardowych:</span><span class="sxs-lookup"><span data-stu-id="f051d-197">Set the following variables to reflect the desired custom collection target configuration:</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-to-a-custom-database-collection-target"></a><span data-ttu-id="f051d-198">Dodawanie baz danych do docelowej kolekcji niestandardowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="f051d-198">Add databases to a custom database collection target</span></span>
<span data-ttu-id="f051d-199">Obiekty docelowe bazy danych mogą być skojarzone z obiektami docelowymi kolekcji niestandardowej bazy danych, aby utworzyć grupę baz danych.</span><span class="sxs-lookup"><span data-stu-id="f051d-199">Database targets can be associated with custom database collection targets to create a group of databases.</span></span> <span data-ttu-id="f051d-200">Zawsze, gdy tworzone jest zadanie cel kolekcji niestandardowej bazy danych, zostanie rozszerzona do bazy danych powiązanych z grupą w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="f051d-200">Whenever a job is created that targets a custom database collection target, it will be expanded to target the databases associated to the group at the time of execution.</span></span>

<span data-ttu-id="f051d-201">Dodaj odpowiednie bazy danych do określonej kolekcji niestandardowych:</span><span class="sxs-lookup"><span data-stu-id="f051d-201">Add the desired database to a specific custom collection:</span></span>

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-the-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="f051d-202">Przejrzyj baz danych w docelowej kolekcji niestandardowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="f051d-202">Review the databases within a custom database collection target</span></span>
<span data-ttu-id="f051d-203">Użyj **Get-AzureSqlJobTarget** polecenia cmdlet, aby pobrać podrzędnej bazy danych w docelowej kolekcji niestandardowej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f051d-203">Use the **Get-AzureSqlJobTarget** cmdlet to retrieve the child databases within a custom database collection target.</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-to-execute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="f051d-204">Utwórz zadanie do wykonania skryptu w docelowej kolekcji niestandardowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="f051d-204">Create a job to execute a script across a custom database collection target</span></span>
<span data-ttu-id="f051d-205">Użyj **AzureSqlJob nowy** polecenia cmdlet można utworzyć zadania w odniesieniu do grupy baz danych, wynika z docelowej kolekcji niestandardowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f051d-205">Use the **New-AzureSqlJob** cmdlet to create a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="f051d-206">Zadania elastyczne bazy danych będzie rozszerzyć zadanie do wielu zadań podrzędnych, odpowiadający każdej bazy danych skojarzony z elementem docelowym kolekcji niestandardowej bazy danych i upewnij się, że skrypt zostanie wykonany w każdej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f051d-206">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span></span> <span data-ttu-id="f051d-207">Ponownie ważne jest, że skrypty są idempotentności pozwala uzyskać odporność na ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="f051d-207">Again, it is important that scripts are idempotent to be resilient to retries.</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a><span data-ttu-id="f051d-208">Zbieranie danych dla baz danych</span><span class="sxs-lookup"><span data-stu-id="f051d-208">Data collection across databases</span></span>
<span data-ttu-id="f051d-209">**Zadania elastyczne bazy danych** obsługuje wykonywanie zapytania na grupę baz danych i wysyła wyników do określonej bazy danych tabeli.</span><span class="sxs-lookup"><span data-stu-id="f051d-209">**Elastic Database jobs** supports executing a query across a group of databases and sends the results to a specified database’s table.</span></span> <span data-ttu-id="f051d-210">Tabela może być badana po fakcie, aby zobaczyć wyniki zapytania w każdej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f051d-210">The table can be queried after the fact to see the query’s results from each database.</span></span> <span data-ttu-id="f051d-211">Zapewnia to asynchronicznego mechanizmu mógł wykonać zapytania przez wiele baz danych.</span><span class="sxs-lookup"><span data-stu-id="f051d-211">This provides an asynchronous mechanism to execute a query across many databases.</span></span> <span data-ttu-id="f051d-212">Błąd przypadkach, takich jak jedna baza danych jest tymczasowo niedostępne są obsługiwane automatycznie za pomocą ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="f051d-212">Failure cases such as one of the databases being temporarily unavailable are handled automatically via retries.</span></span>

<span data-ttu-id="f051d-213">W określonej lokalizacji docelowej tabeli zostaną utworzone automatycznie, jeśli go jeszcze nie istnieje, dopasowania schematu zestaw wyników zwrócony.</span><span class="sxs-lookup"><span data-stu-id="f051d-213">The specified destination table will be automatically created if it does not yet exist, matching the schema of the returned result set.</span></span> <span data-ttu-id="f051d-214">Jeśli wykonanie skrypt zwraca wiele zestawów wyników, zadania elastycznej bazy danych wysyła pierwsza do tabeli docelowej podana.</span><span class="sxs-lookup"><span data-stu-id="f051d-214">If a script execution returns multiple result sets, Elastic Database jobs will only send the first one to the provided destination table.</span></span>

<span data-ttu-id="f051d-215">Poniższy skrypt programu PowerShell może służyć do uruchomienia skryptu zbieranie jej wyników do określonej tabeli.</span><span class="sxs-lookup"><span data-stu-id="f051d-215">The following PowerShell script can be used to execute a script collecting its results into a specified table.</span></span> <span data-ttu-id="f051d-216">Ten skrypt założono, że utworzono skryptu T-SQL, który generuje pojedynczy zestaw wyników i docelowej kolekcji niestandardowej bazie danych została utworzona.</span><span class="sxs-lookup"><span data-stu-id="f051d-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span></span>

<span data-ttu-id="f051d-217">Ustaw następujące polecenie, aby odzwierciedlać żądaną skryptu, poświadczeń i wykonanie docelowego:</span><span class="sxs-lookup"><span data-stu-id="f051d-217">Set the following to reflect the desired script, credentials, and execution target:</span></span>

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

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="f051d-218">Tworzenie i uruchamianie zadania dla scenariuszy zbierania danych</span><span class="sxs-lookup"><span data-stu-id="f051d-218">Create and start a job for data collection scenarios</span></span>
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a><span data-ttu-id="f051d-219">Utwórz harmonogram wykonywania zadania przy użyciu wyzwalacz zadania</span><span class="sxs-lookup"><span data-stu-id="f051d-219">Create a schedule for job execution using a job trigger</span></span>
<span data-ttu-id="f051d-220">Poniższy skrypt programu PowerShell można utworzyć reoccurring harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="f051d-220">The following PowerShell script can be used to create a reoccurring schedule.</span></span> <span data-ttu-id="f051d-221">Ten skrypt używa interwał jedną minutę, ale nowy AzureSqlJobSchedule obsługuje również parametry - DayInterval, - HourInterval i - MonthInterval, - WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="f051d-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="f051d-222">Można utworzyć harmonogramy, które są wykonywane tylko raz przekazywanie przez - jednorazowe.</span><span class="sxs-lookup"><span data-stu-id="f051d-222">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="f051d-223">Utwórz nowy harmonogram:</span><span class="sxs-lookup"><span data-stu-id="f051d-223">Create a new schedule:</span></span>
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-to-have-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="f051d-224">Utwórz wyzwalacz zadania zostały wykonane na harmonogram zadania</span><span class="sxs-lookup"><span data-stu-id="f051d-224">Create a job trigger to have a job executed on a time schedule</span></span>
<span data-ttu-id="f051d-225">Wyzwalacz zadania można definiować zadania wykonywane zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="f051d-225">A job trigger can be defined to have a job executed according to a time schedule.</span></span> <span data-ttu-id="f051d-226">Poniższy skrypt programu PowerShell, można utworzyć wyzwalacza zadania.</span><span class="sxs-lookup"><span data-stu-id="f051d-226">The following PowerShell script can be used to create a job trigger.</span></span>

<span data-ttu-id="f051d-227">Ustaw następujące zmienne odpowiadają żądanego zadania i harmonogramu:</span><span class="sxs-lookup"><span data-stu-id="f051d-227">Set the following variables to correspond to the desired job and schedule:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-to-stop-job-from-executing-on-schedule"></a><span data-ttu-id="f051d-228">Usuń skojarzenie zaplanowane zatrzymania zadania wykonywanie zgodnie z harmonogramem</span><span class="sxs-lookup"><span data-stu-id="f051d-228">Remove a scheduled association to stop job from executing on schedule</span></span>
<span data-ttu-id="f051d-229">Aby przerwać pojawiał wykonywania zadań za pomocą wyzwalacza zadania, można usunąć wyzwalacza zadania.</span><span class="sxs-lookup"><span data-stu-id="f051d-229">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span></span>
<span data-ttu-id="f051d-230">Usuń wyzwalacz zadania zatrzymania zadania z wykonywana zgodnie z harmonogramem przy użyciu **AzureSqlJobTrigger Usuń** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f051d-230">Remove a job trigger to stop a job from being executed according to a schedule using the **Remove-AzureSqlJobTrigger** cmdlet.</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-to-excel"></a><span data-ttu-id="f051d-231">Importuj wyniki zapytania elastycznej bazy danych do programu Excel</span><span class="sxs-lookup"><span data-stu-id="f051d-231">Import elastic database query results to Excel</span></span>
 <span data-ttu-id="f051d-232">Możesz zaimportować wyników zapytania do pliku programu Excel.</span><span class="sxs-lookup"><span data-stu-id="f051d-232">You can import the results from of a query to an Excel file.</span></span>

1. <span data-ttu-id="f051d-233">Uruchom program Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="f051d-233">Launch Excel 2013.</span></span>
2. <span data-ttu-id="f051d-234">Przejdź do **danych** wstążki.</span><span class="sxs-lookup"><span data-stu-id="f051d-234">Navigate to the **Data** ribbon.</span></span>
3. <span data-ttu-id="f051d-235">Kliknij przycisk **z innych źródeł** i kliknij przycisk **z programu SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="f051d-235">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Importowania z programu Excel z innych źródeł](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. <span data-ttu-id="f051d-237">W **Kreator połączenia danych** wpisz poświadczenia, a nazwa logowania serwera.</span><span class="sxs-lookup"><span data-stu-id="f051d-237">In the **Data Connection Wizard** type the server name and login credentials.</span></span> <span data-ttu-id="f051d-238">Następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="f051d-238">Then click **Next**.</span></span>
5. <span data-ttu-id="f051d-239">W oknie dialogowym **wybierz bazę danych, która zawiera dane, które mają**, wybierz pozycję **ElasticDBQuery** bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f051d-239">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="f051d-240">Wybierz **klientów** tabeli w widoku listy, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="f051d-240">Select the **Customers** table in the list view and click **Next**.</span></span> <span data-ttu-id="f051d-241">Następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="f051d-241">Then click **Finish**.</span></span>
7. <span data-ttu-id="f051d-242">W **i zaimportuj dane** formularza, w obszarze **wybierz sposób wyświetlania tych danych w skoroszycie**, wybierz pozycję **tabeli** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f051d-242">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="f051d-243">Wszystkie wiersze z **klientów** tabeli, przechowywane w różnych odłamków wypełnić arkuszu programu Excel.</span><span class="sxs-lookup"><span data-stu-id="f051d-243">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f051d-244">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f051d-244">Next steps</span></span>
<span data-ttu-id="f051d-245">Możesz teraz użyć funkcji danych programu Excel.</span><span class="sxs-lookup"><span data-stu-id="f051d-245">You can now use Excel’s data functions.</span></span> <span data-ttu-id="f051d-246">Umożliwiają parametry połączenia z nazwą serwera, nazwa bazy danych i poświadczeń nawiązanie narzędzi integracji danych i BI kwerendy elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f051d-246">Use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span></span> <span data-ttu-id="f051d-247">Upewnij się, czy program SQL Server jest obsługiwana jako źródło danych dla własnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="f051d-247">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="f051d-248">Zobacz kwerendy elastycznej bazy danych i tabele zewnętrzne, podobnie jak wszystkie inne bazy danych programu SQL Server i tabel programu SQL Server, które można połączyć się z narzędziem.</span><span class="sxs-lookup"><span data-stu-id="f051d-248">Refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="f051d-249">Koszty</span><span class="sxs-lookup"><span data-stu-id="f051d-249">Cost</span></span>
<span data-ttu-id="f051d-250">Brak dodatkowe opłaty za pomocą funkcji zapytania elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f051d-250">There is no additional charge for using the Elastic Database query feature.</span></span> <span data-ttu-id="f051d-251">Jednak w tej chwili ta funkcja jest dostępna tylko w bazach danych premium jako punkt końcowy, ale odłamków może być dowolnym warstwy usługi.</span><span class="sxs-lookup"><span data-stu-id="f051d-251">However, at this time this feature is available only on premium databases as an end point, but the shards can be of any service tier.</span></span>

<span data-ttu-id="f051d-252">Aby uzyskać informacje o cenach zobacz [szczegóły cennika bazy danych SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="f051d-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
