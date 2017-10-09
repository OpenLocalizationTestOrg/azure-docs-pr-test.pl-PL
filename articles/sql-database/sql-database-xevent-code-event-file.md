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
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a>Kod docelowego pliku zdarzenia rozszerzonego zdarzeń w bazie danych SQL

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

Chcesz próbkę kompletny kod dla niezawodny sposób toocapture i przekazuje informacje dla zdarzeń rozszerzonych.

Program Microsoft SQL Server hello [docelowy plik zdarzeń](http://msdn.microsoft.com/library/ff878115.aspx) jest używane toostore wyniki zdarzeń do pliku lokalnego dysku twardego. Jednak takie pliki nie są dostępne tooAzure bazy danych SQL. Zamiast tego użyć hello Azure Storage usługi toosupport hello zdarzeń pliku docelowego.

W tym temacie przedstawiono przykład dwufazowego kodu:

* Środowiska PowerShell toocreate kontenera magazynu Azure w chmurze hello.
* Transact-SQL:
  
  * tooassign hello Azure Storage kontenera tooan zdarzeń pliku docelowego.
  * toocreate i rozpocząć sesji zdarzeń hello i tak dalej.

## <a name="prerequisites"></a>Wymagania wstępne

* Konto i subskrypcja platformy Azure. Po zarejestrowaniu się możesz skorzystać z [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).
* Wszystkie bazy danych, które można utworzyć tabeli.
  
  * Opcjonalnie można [utworzyć **AdventureWorksLT** demonstracyjna baza danych](sql-database-get-started.md) w minutach.
* SQL Server Management Studio (ssms.exe), najlepiej najnowszej miesięcznej wersji aktualizacji. 
  Możesz pobrać najnowszą ssms.exe hello z:
  
  * Temat zatytułowany [pobierania programu SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).
  * [Pobieranie toohello bezpośredniego łącza.](http://go.microsoft.com/fwlink/?linkid=616025)
* Musi mieć hello [modułów programu Azure PowerShell](http://go.microsoft.com/?linkid=9811175) zainstalowane.
  
  * Hello moduły udostępniają poleceń, takich jak - **AzureStorageAccount nowy**.

## <a name="phase-1-powershell-code-for-azure-storage-container"></a>Faza 1: Kod programu PowerShell dla usługi Azure Storage kontenera

Tego programu PowerShell jest przykładowy kod dwufazowego hello faza 1.

skrypt Hello rozpoczyna się od poleceń tooclean po poprzednim potencjalnie Uruchom i jest rerunnable.

1. Wklej hello skrypt programu PowerShell do edytora tekstu prosty przykład Notepad.exe i Zapisz hello skrypt jako plik z rozszerzeniem hello **ps1**.
2. Uruchom ISE programu PowerShell jako Administrator.
3. Wpisz w wierszu hello<br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/>a następnie naciśnij klawisz Enter.
4. Otwórz w programie PowerShell ISE z **ps1** pliku. Uruchom skrypt hello.
5. skrypt Hello pierwszego uruchomienia nowe okno, w którym możesz zalogować się w tooAzure.
   
   * Jeśli uruchomisz hello skryptu bez przerywania sesji istnieje hello opcja wygodny komentowania limit hello **Add-AzureAccount** polecenia.

![PowerShell ISE z modułem Azure zainstalowany, gotowe toorun skryptu.][30_powershell_ise]


### <a name="powershell-code"></a>Kod programu PowerShell

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


Zwróć uwagę na powitania kilka nazwanych wartości, które wyświetla skrypt programu PowerShell powitania po jej zakończeniu. Należy edytować tych wartości do hello skrypt języka Transact-SQL, który następuje fazy 2.

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a>Faza 2: Kod języka Transact-SQL, który używa kontenera magazynu Azure

* W tym przykładowym kodzie faza 1 uruchomiono toocreate skrypt programu PowerShell kontenera magazynu Azure.
* Następnie w Faza 2 hello poniższy skrypt języka Transact-SQL należy użyć hello kontenera.

skrypt Hello rozpoczyna się od poleceń tooclean po poprzednim potencjalnie Uruchom i jest rerunnable.

Witaj skrypt programu PowerShell podane kilka nazwanych wartości czas zakończenia. Należy edytować toouse skryptu języka Transact-SQL hello tych wartości. Znajdź **TODO** w hello języka Transact-SQL skryptu toolocate hello edytować punktów.

1. Otwórz program SQL Server Management Studio (ssms.exe).
2. Połącz tooyour bazy danych z bazy danych SQL Azure.
3. Kliknij przycisk tooopen nowe okienko zapytania.
4. Wklej hello następującego skryptu języka Transact-SQL w okienku kwerendy hello.
5. Znajdź co **TODO** w hello skrypt i wprowadź odpowiednie zmiany hello.
6. Zapisz, a następnie uruchom skrypt hello.


> [!WARNING]
> Witaj SAS wartości klucza wygenerowanych przez hello poprzedzających skrypt programu PowerShell może rozpoczynać się od "?" (znak zapytania). Użycie klucza sygnatury dostępu Współdzielonego hello w hello następującego skryptu T-SQL, należy najpierw *Usuń hello znaku "?"* . W przeciwnym razie wysiłków mogą być blokowane przez zabezpieczenia.


### <a name="transact-sql-code"></a>Kod języka Transact-SQL

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


Jeśli tooattach hello docelowego zakończy się niepowodzeniem, po uruchomieniu, należy zatrzymać i ponownie uruchomić sesji zdarzeń hello:

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a>Dane wyjściowe

Po zakończeniu hello skryptu języka Transact-SQL, kliknij komórkę w obszarze hello **event_data_XML** nagłówka kolumny. Jeden  **<event>**  element jest wyświetlany, która zawiera jedną instrukcję aktualizacji.

Oto jeden  **<event>**  element, który został wygenerowany podczas testowania:


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


Witaj poprzedzających języka Transact-SQL hello skrypt używany po event_file hello tooread funkcji systemu:

* [Funkcja sys.fn_xe_file_target_read_file (Transact-SQL)](http://msdn.microsoft.com/library/cc280743.aspx)

Wyjaśnienie zaawansowane opcje wyświetlania hello danych ze zdarzeń rozszerzonych jest dostępne pod adresem:

* [Zaawansowane wyświetlanie danych docelowych od zdarzeń rozszerzonych](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-hello-code-sample-toorun-on-sql-server"></a>Konwertowanie toorun przykładowy kod hello na serwerze SQL

Załóżmy, że żądana hello toorun poprzedzających próbki języka Transact-SQL w programie Microsoft SQL Server.

* Dla uproszczenia, odpowiedni będzie użycie Zamień toocompletely hello kontenera magazynu Azure przy użyciu prostego pliku takich jak **C:\myeventdata.xel**. Czy można zapisać pliku Hello toohello lokalnym dysku twardym komputera hello, który jest hostem serwera SQL.
* Nie musisz dowolnego rodzaju instrukcji języka Transact-SQL dla **CREATE MASTER KEY** i **poświadczenie tworzenia**.
* W hello **tworzenie zdarzeń sesji** instrukcji w jego **dodać DOCELOWY** klauzuli, należy zastąpić wartość Http hello przypisane wprowadzone za**filename =** z ciągiem pełnej ścieżki, takie jak  **C:\myfile.xel**.
  
  * Muszą być wykonywane żadne konto magazynu Azure.

## <a name="more-information"></a>Więcej informacji

Aby uzyskać więcej informacji o kontach i kontenerów w hello usługi Azure Storage zobacz:

* [Jak toouse magazynu obiektów Blob w .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [Nazewnictwo i odwołuje się do kontenerów, obiektów blob i metadanych](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [Praca z hello nadrzędny kontener](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [Lekcja 1: Utworzenie zasad dostępu przechowywane i sygnatury dostępu współdzielonego kontenera platformy Azure](http://msdn.microsoft.com/library/dn466430.aspx)
  * [Lekcja 2: Tworzenie poświadczeń programu SQL Server przy użyciu sygnatury dostępu współdzielonego](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

