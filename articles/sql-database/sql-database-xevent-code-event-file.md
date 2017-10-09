---
title: "aaaXEvent kodu zdarzeń pliku bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Przykład dwufazowego kod, który demonstruje hello docelowy plik zdarzeń w rozszerzonej zdarzeń w bazie danych SQL Azure zapewnia środowiska PowerShell i języka Transact-SQL. Usługa Azure Storage jest wymagany częścią tego scenariusza."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: bbb10ecc-739f-4159-b844-12b4be161231
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: genemi
ms.openlocfilehash: 4457bd3250f4644b54da2f7daddb9da12070e93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="34d9d-104">Kod docelowego pliku zdarzenia rozszerzonego zdarzeń w bazie danych SQL</span><span class="sxs-lookup"><span data-stu-id="34d9d-104">Event File target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="34d9d-105">Chcesz próbkę kompletny kod dla niezawodny sposób toocapture i przekazuje informacje dla zdarzeń rozszerzonych.</span><span class="sxs-lookup"><span data-stu-id="34d9d-105">You want a complete code sample for a robust way toocapture and report information for an extended event.</span></span>

<span data-ttu-id="34d9d-106">Program Microsoft SQL Server hello [docelowy plik zdarzeń](http://msdn.microsoft.com/library/ff878115.aspx) jest używane toostore wyniki zdarzeń do pliku lokalnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="34d9d-106">In Microsoft SQL Server, hello [Event File target](http://msdn.microsoft.com/library/ff878115.aspx) is used toostore event outputs into a local hard drive file.</span></span> <span data-ttu-id="34d9d-107">Jednak takie pliki nie są dostępne tooAzure bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="34d9d-107">But such files are not available tooAzure SQL Database.</span></span> <span data-ttu-id="34d9d-108">Zamiast tego użyć hello Azure Storage usługi toosupport hello zdarzeń pliku docelowego.</span><span class="sxs-lookup"><span data-stu-id="34d9d-108">Instead we use hello Azure Storage service toosupport hello Event File target.</span></span>

<span data-ttu-id="34d9d-109">W tym temacie przedstawiono przykład dwufazowego kodu:</span><span class="sxs-lookup"><span data-stu-id="34d9d-109">This topic presents a two-phase code sample:</span></span>

* <span data-ttu-id="34d9d-110">Środowiska PowerShell toocreate kontenera magazynu Azure w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="34d9d-110">PowerShell, toocreate an Azure Storage container in hello cloud.</span></span>
* <span data-ttu-id="34d9d-111">Transact-SQL:</span><span class="sxs-lookup"><span data-stu-id="34d9d-111">Transact-SQL:</span></span>
  
  * <span data-ttu-id="34d9d-112">tooassign hello Azure Storage kontenera tooan zdarzeń pliku docelowego.</span><span class="sxs-lookup"><span data-stu-id="34d9d-112">tooassign hello Azure Storage container tooan Event File target.</span></span>
  * <span data-ttu-id="34d9d-113">toocreate i rozpocząć sesji zdarzeń hello i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="34d9d-113">toocreate and start hello event session, and so on.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34d9d-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="34d9d-114">Prerequisites</span></span>

* <span data-ttu-id="34d9d-115">Konto i subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="34d9d-115">An Azure account and subscription.</span></span> <span data-ttu-id="34d9d-116">Po zarejestrowaniu się możesz skorzystać z [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="34d9d-116">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="34d9d-117">Wszystkie bazy danych, które można utworzyć tabeli.</span><span class="sxs-lookup"><span data-stu-id="34d9d-117">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="34d9d-118">Opcjonalnie można [utworzyć **AdventureWorksLT** demonstracyjna baza danych](sql-database-get-started.md) w minutach.</span><span class="sxs-lookup"><span data-stu-id="34d9d-118">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="34d9d-119">SQL Server Management Studio (ssms.exe), najlepiej najnowszej miesięcznej wersji aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="34d9d-119">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="34d9d-120">Możesz pobrać najnowszą ssms.exe hello z:</span><span class="sxs-lookup"><span data-stu-id="34d9d-120">You can download hello latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="34d9d-121">Temat zatytułowany [pobierania programu SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="34d9d-121">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="34d9d-122">Pobieranie toohello bezpośredniego łącza.</span><span class="sxs-lookup"><span data-stu-id="34d9d-122">A direct link toohello download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)
* <span data-ttu-id="34d9d-123">Musi mieć hello [modułów programu Azure PowerShell](http://go.microsoft.com/?linkid=9811175) zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="34d9d-123">You must have hello [Azure PowerShell modules](http://go.microsoft.com/?linkid=9811175) installed.</span></span>
  
  * <span data-ttu-id="34d9d-124">Hello moduły udostępniają poleceń, takich jak - **AzureStorageAccount nowy**.</span><span class="sxs-lookup"><span data-stu-id="34d9d-124">hello modules provide commands such as - **New-AzureStorageAccount**.</span></span>

## <a name="phase-1-powershell-code-for-azure-storage-container"></a><span data-ttu-id="34d9d-125">Faza 1: Kod programu PowerShell dla usługi Azure Storage kontenera</span><span class="sxs-lookup"><span data-stu-id="34d9d-125">Phase 1: PowerShell code for Azure Storage container</span></span>

<span data-ttu-id="34d9d-126">Tego programu PowerShell jest przykładowy kod dwufazowego hello faza 1.</span><span class="sxs-lookup"><span data-stu-id="34d9d-126">This PowerShell is phase 1 of hello two-phase code sample.</span></span>

<span data-ttu-id="34d9d-127">skrypt Hello rozpoczyna się od poleceń tooclean po poprzednim potencjalnie Uruchom i jest rerunnable.</span><span class="sxs-lookup"><span data-stu-id="34d9d-127">hello script starts with commands tooclean up after a possible previous run, and is rerunnable.</span></span>

1. <span data-ttu-id="34d9d-128">Wklej hello skrypt programu PowerShell do edytora tekstu prosty przykład Notepad.exe i Zapisz hello skrypt jako plik z rozszerzeniem hello **ps1**.</span><span class="sxs-lookup"><span data-stu-id="34d9d-128">Paste hello PowerShell script into a simple text editor such as Notepad.exe, and save hello script as a file with hello extension **.ps1**.</span></span>
2. <span data-ttu-id="34d9d-129">Uruchom ISE programu PowerShell jako Administrator.</span><span class="sxs-lookup"><span data-stu-id="34d9d-129">Start PowerShell ISE as an Administrator.</span></span>
3. <span data-ttu-id="34d9d-130">Wpisz w wierszu hello</span><span class="sxs-lookup"><span data-stu-id="34d9d-130">At hello prompt, type</span></span><br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/><span data-ttu-id="34d9d-131">a następnie naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="34d9d-131">and then press Enter.</span></span>
4. <span data-ttu-id="34d9d-132">Otwórz w programie PowerShell ISE z **ps1** pliku.</span><span class="sxs-lookup"><span data-stu-id="34d9d-132">In PowerShell ISE, open your **.ps1** file.</span></span> <span data-ttu-id="34d9d-133">Uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="34d9d-133">Run hello script.</span></span>
5. <span data-ttu-id="34d9d-134">skrypt Hello pierwszego uruchomienia nowe okno, w którym możesz zalogować się w tooAzure.</span><span class="sxs-lookup"><span data-stu-id="34d9d-134">hello script first starts a new window in which you log in tooAzure.</span></span>
   
   * <span data-ttu-id="34d9d-135">Jeśli uruchomisz hello skryptu bez przerywania sesji istnieje hello opcja wygodny komentowania limit hello **Add-AzureAccount** polecenia.</span><span class="sxs-lookup"><span data-stu-id="34d9d-135">If you rerun hello script without disrupting your session, you have hello convenient option of commenting out hello **Add-AzureAccount** command.</span></span>

![PowerShell ISE z modułem Azure zainstalowany, gotowe toorun skryptu.][30_powershell_ise]


### <a name="powershell-code"></a><span data-ttu-id="34d9d-137">Kod programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="34d9d-137">PowerShell code</span></span>

```powershell
## TODO: Before running, find all 'TODO' and make each edit!!

#--------------- 1 -----------------------


# You can comment out or skip this Add-AzureAccount
# command after hello first run.
# Current PowerShell environment retains hello successful outcome.

'Expect a pop-up window in which you log in tooAzure.'


Add-AzureAccount

#-------------- 2 ------------------------


'
TODO: Edit hello values assigned toothese variables, especially hello first few!
'

# Ensure hello current date is between
# hello Expiry and Start time values that you edit here.

$subscriptionName    = 'YOUR_SUBSCRIPTION_NAME'
$policySasExpiryTime = '2016-01-28T23:44:56Z'
$policySasStartTime  = '2015-08-01'


$storageAccountName     = 'gmstorageaccountxevent'
$storageAccountLocation = 'West US'
$contextName            = 'gmcontext'
$containerName          = 'gmcontainerxevent'
$policySasToken         = 'gmpolicysastoken'


# Leave this value alone, as 'rwl'.
$policySasPermission = 'rwl'

#--------------- 3 -----------------------


# hello ending display lists your Azure subscriptions.
# One should match hello $subscriptionName value you assigned
#   earlier in this PowerShell script. 

'Choose an existing subscription for hello current PowerShell environment.'


Select-AzureSubscription -SubscriptionName $subscriptionName


#-------------- 4 ------------------------


'
Clean up hello old Azure Storage Account after any previous run, 
before continuing this new run.'


If ($storageAccountName)
{
    Remove-AzureStorageAccount -StorageAccountName $storageAccountName
}

#--------------- 5 -----------------------

[System.DateTime]::Now.ToString()

'
Create a storage account. 
This might take several minutes, will beep when ready.
  ...PLEASE WAIT...'

New-AzureStorageAccount `
    -StorageAccountName $storageAccountName `
    -Location           $storageAccountLocation

[System.DateTime]::Now.ToString()

[System.Media.SystemSounds]::Beep.Play()


'
Get hello primary access key for your storage account.
'


$primaryAccessKey_ForStorageAccount = `
    (Get-AzureStorageKey `
        -StorageAccountName $storageAccountName).Primary

"`$primaryAccessKey_ForStorageAccount = $primaryAccessKey_ForStorageAccount"

'Azure Storage Account cmdlet completed.
Remainder of PowerShell .ps1 script continues.
'

#--------------- 6 -----------------------


# hello context will be needed toocreate a container within hello storage account.

'Create a context object from hello storage account and its primary access key.
'

$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey  $primaryAccessKey_ForStorageAccount


'Create a container within hello storage account.
'


$containerObjectInStorageAccount = New-AzureStorageContainer `
    -Name    $containerName `
    -Context $context


'Create a security policy toobe applied toohello SAS token.
'

New-AzureStorageContainerStoredAccessPolicy `
    -Container  $containerName `
    -Context    $context `
    -Policy     $policySasToken `
    -Permission $policySasPermission `
    -ExpiryTime $policySasExpiryTime `
    -StartTime  $policySasStartTime 

'
Generate a SAS token for hello container.
'
Try
{
    $sasTokenWithPolicy = New-AzureStorageContainerSASToken `
        -Name    $containerName `
        -Context $context `
        -Policy  $policySasToken
}
Catch 
{
    $Error[0].Exception.ToString()
}

#-------------- 7 ------------------------


'Display hello values that YOU must edit into hello Transact-SQL script next!:
'

"storageAccountName: $storageAccountName"
"containerName:      $containerName"
"sasTokenWithPolicy: $sasTokenWithPolicy"

'
REMINDER: sasTokenWithPolicy here might start with "?" character, which you must exclude from Transact-SQL.
'

'
(Later, return here toodelete your Azure Storage account. See hello preceding - Remove-AzureStorageAccount -StorageAccountName $storageAccountName)'

'
Now shift toohello Transact-SQL portion of hello two-part code sample!'

# EOFile
```


<span data-ttu-id="34d9d-138">Zwróć uwagę na powitania kilka nazwanych wartości, które wyświetla skrypt programu PowerShell powitania po jej zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="34d9d-138">Take note of hello few named values that hello PowerShell script prints when it ends.</span></span> <span data-ttu-id="34d9d-139">Należy edytować tych wartości do hello skrypt języka Transact-SQL, który następuje fazy 2.</span><span class="sxs-lookup"><span data-stu-id="34d9d-139">You must edit those values into hello Transact-SQL script that follows as phase 2.</span></span>

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a><span data-ttu-id="34d9d-140">Faza 2: Kod języka Transact-SQL, który używa kontenera magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="34d9d-140">Phase 2: Transact-SQL code that uses Azure Storage container</span></span>

* <span data-ttu-id="34d9d-141">W tym przykładowym kodzie faza 1 uruchomiono toocreate skrypt programu PowerShell kontenera magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="34d9d-141">In phase 1 of this code sample, you ran a PowerShell script toocreate an Azure Storage container.</span></span>
* <span data-ttu-id="34d9d-142">Następnie w Faza 2 hello poniższy skrypt języka Transact-SQL należy użyć hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="34d9d-142">Next in phase 2, hello following Transact-SQL script must use hello container.</span></span>

<span data-ttu-id="34d9d-143">skrypt Hello rozpoczyna się od poleceń tooclean po poprzednim potencjalnie Uruchom i jest rerunnable.</span><span class="sxs-lookup"><span data-stu-id="34d9d-143">hello script starts with commands tooclean up after a possible previous run, and is rerunnable.</span></span>

<span data-ttu-id="34d9d-144">Witaj skrypt programu PowerShell podane kilka nazwanych wartości czas zakończenia.</span><span class="sxs-lookup"><span data-stu-id="34d9d-144">hello PowerShell script printed a few named values when it ended.</span></span> <span data-ttu-id="34d9d-145">Należy edytować toouse skryptu języka Transact-SQL hello tych wartości.</span><span class="sxs-lookup"><span data-stu-id="34d9d-145">You must edit hello Transact-SQL script toouse those values.</span></span> <span data-ttu-id="34d9d-146">Znajdź **TODO** w hello języka Transact-SQL skryptu toolocate hello edytować punktów.</span><span class="sxs-lookup"><span data-stu-id="34d9d-146">Find **TODO** in hello Transact-SQL script toolocate hello edit points.</span></span>

1. <span data-ttu-id="34d9d-147">Otwórz program SQL Server Management Studio (ssms.exe).</span><span class="sxs-lookup"><span data-stu-id="34d9d-147">Open SQL Server Management Studio (ssms.exe).</span></span>
2. <span data-ttu-id="34d9d-148">Połącz tooyour bazy danych z bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="34d9d-148">Connect tooyour Azure SQL Database database.</span></span>
3. <span data-ttu-id="34d9d-149">Kliknij przycisk tooopen nowe okienko zapytania.</span><span class="sxs-lookup"><span data-stu-id="34d9d-149">Click tooopen a new query pane.</span></span>
4. <span data-ttu-id="34d9d-150">Wklej hello następującego skryptu języka Transact-SQL w okienku kwerendy hello.</span><span class="sxs-lookup"><span data-stu-id="34d9d-150">Paste hello following Transact-SQL script into hello query pane.</span></span>
5. <span data-ttu-id="34d9d-151">Znajdź co **TODO** w hello skrypt i wprowadź odpowiednie zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="34d9d-151">Find every **TODO** in hello script and make hello appropriate edits.</span></span>
6. <span data-ttu-id="34d9d-152">Zapisz, a następnie uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="34d9d-152">Save, and then run hello script.</span></span>


> [!WARNING]
> <span data-ttu-id="34d9d-153">Witaj SAS wartości klucza wygenerowanych przez hello poprzedzających skrypt programu PowerShell może rozpoczynać się od "?" (znak zapytania).</span><span class="sxs-lookup"><span data-stu-id="34d9d-153">hello SAS key value generated by hello preceding PowerShell script might begin with a '?' (question mark).</span></span> <span data-ttu-id="34d9d-154">Użycie klucza sygnatury dostępu Współdzielonego hello w hello następującego skryptu T-SQL, należy najpierw *Usuń hello znaku "?"* .</span><span class="sxs-lookup"><span data-stu-id="34d9d-154">When you use hello SAS key in hello following T-SQL script, you must *remove hello leading '?'*.</span></span> <span data-ttu-id="34d9d-155">W przeciwnym razie wysiłków mogą być blokowane przez zabezpieczenia.</span><span class="sxs-lookup"><span data-stu-id="34d9d-155">Otherwise your efforts might be blocked by security.</span></span>


### <a name="transact-sql-code"></a><span data-ttu-id="34d9d-156">Kod języka Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="34d9d-156">Transact-SQL code</span></span>

```sql
---- TODO: First, run hello PowerShell portion of this two-part code sample.
---- TODO: Second, find every 'TODO' in this Transact-SQL file, and edit each.

---- Transact-SQL code for Event File target on Azure SQL Database.


SET NOCOUNT ON;
GO


----  Step 1.  Establish one little table, and  ---------
----  insert one row of data.


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'gmTabEmployee')
BEGIN
    DROP TABLE gmTabEmployee;
END
GO


CREATE TABLE gmTabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO gmTabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO


------  Step 2.  Create key, and  ------------
------  Create credential (your Azure Storage container must already exist).


IF NOT EXISTS
    (SELECT * FROM sys.symmetric_keys
        WHERE symmetric_key_id = 101)
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '0C34C960-6621-4682-A123-C7EA08E3FC46' -- Or any newid().
END
GO


IF EXISTS
    (SELECT * FROM sys.database_scoped_credentials
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        WHERE name = 'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent')
BEGIN
    DROP DATABASE SCOPED CREDENTIAL
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent] ;
END
GO


CREATE
    DATABASE SCOPED
    CREDENTIAL
        -- use '.blob.',   and not '.queue.' or '.table.' etc.
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    WITH
        IDENTITY = 'SHARED ACCESS SIGNATURE',  -- "SAS" token.
        -- TODO: Paste in hello long SasToken string here for Secret, but exclude any leading '?'.
        SECRET = 'sv=2014-02-14&sr=c&si=gmpolicysastoken&sig=EjAqjo6Nu5xMLEZEkMkLbeF7TD9v1J8DNB2t8gOKTts%3D'
    ;
GO


------  Step 3.  Create (define) an event session.  --------
------  hello event session has an event with an action,
------  and a has a target.

IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'gmeventsessionname240b')
BEGIN
    DROP
        EVENT SESSION
            gmeventsessionname240b
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE

    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE 'UPDATE gmTabEmployee%'
            )
    ADD TARGET
        package0.event_file
            (
            -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
            -- Also, tweak hello .xel file name at end, if you like.
            SET filename =
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b.xel'
            )
    WITH
        (MAX_MEMORY = 10 MB,
        MAX_DISPATCH_LATENCY = 3 SECONDS)
    ;
GO


------  Step 4.  Start hello event session.  ----------------
------  Issue hello SQL Update statements that will be traced.
------  Then stop hello session.

------  Note: If hello target fails tooattach,
------  hello session must be stopped and restarted.

ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = START;
GO


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
GO


ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = STOP;
GO


-------------- Step 5.  Select hello results. ----------

SELECT
        *, 'CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS!' as [CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS],
        CAST(event_data AS XML) AS [event_data_XML]  -- TODO: In ssms.exe results grid, double-click this cell!
    FROM
        sys.fn_xe_file_target_read_file
            (
                -- TODO: Fill in Storage Account name, and hello associated Container name.
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b',
                null, null, null
            );
GO


-------------- Step 6.  Clean up. ----------

DROP
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE;
GO

DROP DATABASE SCOPED CREDENTIAL
    -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
    [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    ;
GO

DROP TABLE gmTabEmployee;
GO

PRINT 'Use PowerShell Remove-AzureStorageAccount toodelete your Azure Storage account!';
GO
```


<span data-ttu-id="34d9d-157">Jeśli tooattach hello docelowego zakończy się niepowodzeniem, po uruchomieniu, należy zatrzymać i ponownie uruchomić sesji zdarzeń hello:</span><span class="sxs-lookup"><span data-stu-id="34d9d-157">If hello target fails tooattach when you run, you must stop and restart hello event session:</span></span>

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a><span data-ttu-id="34d9d-158">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="34d9d-158">Output</span></span>

<span data-ttu-id="34d9d-159">Po zakończeniu hello skryptu języka Transact-SQL, kliknij komórkę w obszarze hello **event_data_XML** nagłówka kolumny.</span><span class="sxs-lookup"><span data-stu-id="34d9d-159">When hello Transact-SQL script completes, click a cell under hello **event_data_XML** column header.</span></span> <span data-ttu-id="34d9d-160">Jeden  **<event>**  element jest wyświetlany, która zawiera jedną instrukcję aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="34d9d-160">One **<event>** element is displayed which shows one UPDATE statement.</span></span>

<span data-ttu-id="34d9d-161">Oto jeden  **<event>**  element, który został wygenerowany podczas testowania:</span><span class="sxs-lookup"><span data-stu-id="34d9d-161">Here is one **<event>** element that was generated during testing:</span></span>


```xml
<event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T19:18:45.420Z">
  <data name="state">
    <value>0</value>
    <text>Normal</text>
  </data>
  <data name="line_number">
    <value>5</value>
  </data>
  <data name="offset">
    <value>148</value>
  </data>
  <data name="offset_end">
    <value>368</value>
  </data>
  <data name="statement">
    <value>UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe'</value>
  </data>
  <action name="sql_text" package="sqlserver">
    <value>

SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
</value>
  </action>
</event>
```


<span data-ttu-id="34d9d-162">Witaj poprzedzających języka Transact-SQL hello skrypt używany po event_file hello tooread funkcji systemu:</span><span class="sxs-lookup"><span data-stu-id="34d9d-162">hello preceding Transact-SQL script used hello following system function tooread hello event_file:</span></span>

* [<span data-ttu-id="34d9d-163">Funkcja sys.fn_xe_file_target_read_file (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="34d9d-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/cc280743.aspx)

<span data-ttu-id="34d9d-164">Wyjaśnienie zaawansowane opcje wyświetlania hello danych ze zdarzeń rozszerzonych jest dostępne pod adresem:</span><span class="sxs-lookup"><span data-stu-id="34d9d-164">An explanation of advanced options for hello viewing of data from extended events is available at:</span></span>

* [<span data-ttu-id="34d9d-165">Zaawansowane wyświetlanie danych docelowych od zdarzeń rozszerzonych</span><span class="sxs-lookup"><span data-stu-id="34d9d-165">Advanced Viewing of Target Data from Extended Events</span></span>](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-hello-code-sample-toorun-on-sql-server"></a><span data-ttu-id="34d9d-166">Konwertowanie toorun przykładowy kod hello na serwerze SQL</span><span class="sxs-lookup"><span data-stu-id="34d9d-166">Converting hello code sample toorun on SQL Server</span></span>

<span data-ttu-id="34d9d-167">Załóżmy, że żądana hello toorun poprzedzających próbki języka Transact-SQL w programie Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="34d9d-167">Suppose you wanted toorun hello preceding Transact-SQL sample on Microsoft SQL Server.</span></span>

* <span data-ttu-id="34d9d-168">Dla uproszczenia, odpowiedni będzie użycie Zamień toocompletely hello kontenera magazynu Azure przy użyciu prostego pliku takich jak **C:\myeventdata.xel**.</span><span class="sxs-lookup"><span data-stu-id="34d9d-168">For simplicity, you would want toocompletely replace use of hello Azure Storage container with a simple file such as **C:\myeventdata.xel**.</span></span> <span data-ttu-id="34d9d-169">Czy można zapisać pliku Hello toohello lokalnym dysku twardym komputera hello, który jest hostem serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="34d9d-169">hello file would be written toohello local hard drive of hello computer that hosts SQL Server.</span></span>
* <span data-ttu-id="34d9d-170">Nie musisz dowolnego rodzaju instrukcji języka Transact-SQL dla **CREATE MASTER KEY** i **poświadczenie tworzenia**.</span><span class="sxs-lookup"><span data-stu-id="34d9d-170">You would not need any kind of Transact-SQL statements for **CREATE MASTER KEY** and **CREATE CREDENTIAL**.</span></span>
* <span data-ttu-id="34d9d-171">W hello **tworzenie zdarzeń sesji** instrukcji w jego **dodać DOCELOWY** klauzuli, należy zastąpić wartość Http hello przypisane wprowadzone za**filename =** z ciągiem pełnej ścieżki, takie jak  **C:\myfile.xel**.</span><span class="sxs-lookup"><span data-stu-id="34d9d-171">In hello **CREATE EVENT SESSION** statement, in its **ADD TARGET** clause, you would replace hello Http value assigned made too**filename=** with a full path string like **C:\myfile.xel**.</span></span>
  
  * <span data-ttu-id="34d9d-172">Muszą być wykonywane żadne konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="34d9d-172">No Azure Storage account need be involved.</span></span>

## <a name="more-information"></a><span data-ttu-id="34d9d-173">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="34d9d-173">More information</span></span>

<span data-ttu-id="34d9d-174">Aby uzyskać więcej informacji o kontach i kontenerów w hello usługi Azure Storage zobacz:</span><span class="sxs-lookup"><span data-stu-id="34d9d-174">For more info about accounts and containers in hello Azure Storage service, see:</span></span>

* [<span data-ttu-id="34d9d-175">Jak toouse magazynu obiektów Blob w .NET</span><span class="sxs-lookup"><span data-stu-id="34d9d-175">How toouse Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="34d9d-176">Nazewnictwo i odwołuje się do kontenerów, obiektów blob i metadanych</span><span class="sxs-lookup"><span data-stu-id="34d9d-176">Naming and Referencing Containers, Blobs, and Metadata</span></span>](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [<span data-ttu-id="34d9d-177">Praca z hello nadrzędny kontener</span><span class="sxs-lookup"><span data-stu-id="34d9d-177">Working with hello Root Container</span></span>](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [<span data-ttu-id="34d9d-178">Lekcja 1: Utworzenie zasad dostępu przechowywane i sygnatury dostępu współdzielonego kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="34d9d-178">Lesson 1: Create a stored access policy and a shared access signature on an Azure container</span></span>](http://msdn.microsoft.com/library/dn466430.aspx)
  * [<span data-ttu-id="34d9d-179">Lekcja 2: Tworzenie poświadczeń programu SQL Server przy użyciu sygnatury dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="34d9d-179">Lesson 2: Create a SQL Server credential using a shared access signature</span></span>](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

