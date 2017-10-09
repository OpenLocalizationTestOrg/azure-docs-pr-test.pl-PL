---
title: "aaaCreate elastycznej zadania przy użyciu programu PowerShell i zarządzać nimi | Dokumentacja firmy Microsoft"
description: "PowerShell używane toomanage pule bazy danych SQL Azure"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a>Tworzenie i zarządzanie nimi zadania elastycznej bazy danych SQL przy użyciu programu PowerShell (wersja zapoznawcza)

Witaj interfejsów API środowiska PowerShell dla **zadania elastycznej bazy danych** (w wersji zapoznawczej), umożliwiają definiowanie grupę baz danych, które wykona skryptów. W tym artykule przedstawiono sposób toocreate i zarządzanie nimi **zadania elastycznej bazy danych** przy użyciu poleceń cmdlet programu PowerShell. Zobacz [omówienie zadania elastyczne](sql-database-elastic-jobs-overview.md). 

## <a name="prerequisites"></a>Wymagania wstępne
* Subskrypcja platformy Azure. Bezpłatnej wersji próbnej, zobacz [bezpłatna miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).
* Zestaw baz danych utworzonych z hello narzędzi elastycznej bazy danych. Zobacz [wprowadzenie do narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).
* Azure PowerShell. Aby uzyskać szczegółowe informacje, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).
* **Zadania elastyczne bazy danych** pakietu programu PowerShell: zobacz [zadania instalowania elastycznej bazy danych](sql-database-elastic-jobs-service-installation.md)

### <a name="select-your-azure-subscription"></a>Wybierz subskrypcję platformy Azure
tooselect hello subskrypcji należy identyfikator subskrypcji (**- SubscriptionId**) lub nazwę subskrypcji (**— Nazwa subskrypcji**). Jeśli masz wiele subskrypcji możesz uruchomić hello **Get-AzureRmSubscription** polecenia cmdlet i skopiuj hello potrzeby informacji o subskrypcji z hello zestawu wyników. Po uzyskaniu informacji o subskrypcji, uruchom następujące polecenie commandlet tooset hello tej subskrypcji jako domyślny hello, a mianowicie hello cel dla tworzenia zadania i zarządzać nimi:

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

Witaj [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) jest zalecane w przypadku użycia toodevelop i wykonywanie skryptów programu PowerShell przed hello zadania elastycznej bazy danych.

## <a name="elastic-database-jobs-objects"></a>Obiekty zadania elastycznej bazy danych
Witaj następujących tabela zawiera listę się wszystkie typy obiektów hello z **zadania elastycznej bazy danych** wraz z jego opis i odpowiednich interfejsów API programu PowerShell.

<table style="width:100%">
  <tr>
    <th>Typ obiektu</th>
    <th>Opis</th>
    <th>Powiązanych interfejsów API programu PowerShell</th>
  </tr>
  <tr>
    <td>Poświadczenie</td>
    <td>Toouse nazwy użytkownika i hasła podczas łączenia toodatabases dla wykonywania skryptów lub aplikacji DACPACs. <p>Witaj hasło jest szyfrowane przed wysłaniem tooand przechowywania w hello zadania elastyczne bazy danych w bazie danych.  hasło Hello jest odszyfrowywany przez hello zadania elastyczne bazy danych usługi za pomocą poświadczeń hello utworzone i załadowane z hello skrypt instalacji.</td>
    <td><p>Get-AzureSqlJobCredential</p>
    <p>Nowe AzureSqlJobCredential</p><p>Zestaw AzureSqlJobCredential</p></td></td>
  </tr>

  <tr>
    <td>Skrypt</td>
    <td>Toobe skryptu języka Transact-SQL używane do wykonywania różnych bazach danych.  skrypt Hello powinna być idempotentności toobe utworzone, ponieważ usługa hello ponowi wykonanie skryptu powitania po awarii.
    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>Get-AzureSqlJobContentDefinition</p>
    <p>Nowe AzureSqlJobContent</p>
    <p>Zestaw AzureSqlJobContentDefinition</p>
    </td>
  </tr>

  <tr>
    <td>DACPAC</td>
    <td><a href="https://msdn.microsoft.com/library/ee210546.aspx">Aplikacji warstwy danych </a> pakietu toobe zastosowany do wszystkich baz danych.

    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>Nowe AzureSqlJobContent</p>
    <p>Zestaw AzureSqlJobContentDefinition</p>
    </td>
  </tr>
  <tr>
    <td>Docelowej bazy danych</td>
    <td>Bazy danych i serwera nazw tooan wskazujące bazę danych SQL Azure.

    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>Nowe AzureSqlJobTarget</p>
    </td>
  </tr>
  <tr>
    <td>Identyfikator niezależnego fragmentu mapy docelowego</td>
    <td>Kombinacja docelowej bazy danych i toobe poświadczenia używane toodetermine informacje przechowywane w mapie niezależnego fragmentu elastycznej bazy danych.
    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>Nowe AzureSqlJobTarget</p>
    <p>Zestaw AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>Docelowy kolekcji niestandardowej</td>
    <td>Zdefiniowaną grupę toocollectively baz danych użycia dla wykonania.</td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>Nowe AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>Docelowy podrzędnej kolekcji niestandardowej</td>
    <td>Obiekt docelowy bazy danych, do którego odwołuje się z kolekcji niestandardowej.</td>
    <td>
    <p>Dodaj AzureSqlJobChildTarget</p>
    <p>Usuń AzureSqlJobChildTarget</p>
    </td>
  </tr>

<tr>
    <td>Zadanie</td>
    <td>
    <p>Definicja parametrów dla zadania, które mogą być używane tootrigger wykonanie lub toofulfill harmonogram.</p>
    </td>
    <td>
    <p>Get-AzureSqlJob</p>
    <p>Nowe AzureSqlJob</p>
    <p>Zestaw AzureSqlJob</p>
    </td>
  </tr>

<tr>
    <td>Wykonanie zadania</td>
    <td>
    <p>Kontener toofulfill niezbędnych zadań wykonywania skryptu lub zastosowania docelowego tooa DACPAC, przy użyciu poświadczeń dla połączenia z bazą danych z błędami obsługiwane zasady wykonywania tooan zgodnie.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>AzureSqlJobExecution oczekiwania</p>
  </tr>

<tr>
    <td>Wykonywanie zadań zadania</td>
    <td>
    <p>Pojedynczą jednostkę pracy toofulfill zadania.</p>
    <p>Jeśli zadanie nie jest możliwe toosuccessfully wykonania, będą rejestrowane hello Wynikowy komunikat o wyjątku i nowe zadanie dopasowania zostanie utworzona i wykonywane w określonych toohello zgodnie zasad wykonywania.</p></p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>AzureSqlJobExecution oczekiwania</p>
  </tr>

<tr>
    <td>Zasady wykonywania zadania</td>
    <td>
    <p>Formanty zadań limitów czasu wykonywania, ponownych prób, ograniczenia i odstępach czasu między kolejnymi próbami.</p>
    <p>Zadania elastyczne bazy danych zawiera domyślne zasady wykonywania zadania, które zasadniczo nieskończone ponowne próby niepowodzeń zadań zadania z wykładniczego wycofywania odstępach czasu między kolejnymi próbami.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecutionPolicy</p>
    <p>Nowe AzureSqlJobExecutionPolicy</p>
    <p>Zestaw AzureSqlJobExecutionPolicy</p>
    </td>
  </tr>

<tr>
    <td>Harmonogram</td>
    <td>
    <p>Czas na podstawie specyfikacji wykonywania tootake miejsce reoccurring interwał lub na jeden raz.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobSchedule</p>
    <p>Nowe AzureSqlJobSchedule</p>
    <p>Zestaw AzureSqlJobSchedule</p>
    </td>
  </tr>

<tr>
    <td>Wyzwala zadanie</td>
    <td>
    <p>Mapowanie między zadania i harmonogram wykonywania zadania tootrigger zgodnie z harmonogramem toohello.</p>
    </td>
    <td>
    <p>Nowe AzureSqlJobTrigger</p>
    <p>Usuń AzureSqlJobTrigger</p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a>Obsługiwane zadania elastycznej bazy danych grupy typów
zadanie Hello wykonuje skrypty języka Transact-SQL (T-SQL) lub aplikacji DACPACs między grupą baz danych. Gdy zadanie jest przesłanych toobe wykonywane przez grupę baz danych, zadania hello "rozwija" hello na zadań podrzędnych, gdzie pełniących hello zażądał miało zostać wykonane w pojedynczej bazy danych w grupie hello. 

Istnieją dwa typy grup, które możesz utworzyć: 

* [Mapa niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md) grupy: zadania po przesłanych tootarget mapy niezależnego fragmentu zadania hello odpytuje hello niezależnego fragmentu mapy toodetermine jej bieżącego zestawu odłamków, a następnie zadania dla każdego niezależnego fragmentu tworzy podrzędnych, hello niezależnego fragmentu mapy.
* Niestandardowe grupy zbierania: niestandardowy zdefiniowany zestaw baz danych. Gdy zadanie jest przeznaczony dla kolekcji niestandardowych, tworzy podrzędnych zadania dla każdej bazy danych obecnie w kolekcji niestandardowej hello.

## <a name="tooset-hello-elastic-database-jobs-connection"></a>Witaj tooset połączenia zadania elastycznej bazy danych
Połączenie musi toobe Konfigurowanie toohello zadań *bazy danych kontroli* hello toousing poprzedniego zadania interfejsów API. Uruchomienie tego polecenia cmdlet wyzwala toopop okna poświadczeń, się Żądanie hello nazwy użytkownika i hasła utworzonego podczas instalacji zadania elastycznej bazy danych. Wszystkie przykłady w tym temacie założono, że pierwsza została już wykonana.

Otwórz połączenie toohello elastycznej bazy danych zadań:

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a>Zaszyfrowane poświadczenia w ramach hello zadania elastycznej bazy danych
Poświadczenia bazy danych można wstawiać do zadań hello *bazy danych kontroli* jego hasłem, szyfrowane. Jest toostore niezbędne poświadczenia tooenable zadania toobe wykonane w późniejszym czasie (przy użyciu harmonogramy zadań).

Szyfrowanie działa za pośrednictwem utworzone jako część hello skrypt instalacji certyfikatu. Tworzy skrypt instalacji Hello i przekazywanie certyfikatu hello na powitania usługi w chmurze Azure do odszyfrowywania hello przechowywane hasła szyfrowane. Usługi w chmurze Azure Hello później przechowuje hello klucza publicznego w ramach zadania hello *bazy danych kontroli* co pozwala hello interfejsu API programu PowerShell lub klasycznego portalu Azure tooencrypt interfejsu podanego hasła bez konieczności hello certyfikatu toobe zainstalowane lokalnie.

Witaj poświadczenie hasła są szyfrowane i bezpieczne od użytkowników z obiektami zadania bazy danych tooElastic dostęp tylko do odczytu. Ale istnieje możliwość przez złośliwego użytkownika mającego dostęp do odczytu zapisu tooElastic zadań baz danych obiektów tooextract hasła. Poświadczenia są zaprojektowane toobe ponownie wykorzystać w odniesieniu do wykonania zadania. Poświadczenia są przekazywane tootarget baz danych podczas ustanawiania połączenia. Obecnie nie istnieją żadne ograniczenia dotyczące hello docelowymi bazami danych używane dla każdego poświadczenia, złośliwy użytkownik może dodać element docelowy bazy danych dla bazy danych pod kontrolą hello złośliwy użytkownik. Użytkownik Hello później można uruchomić zadania przeznaczonych dla tej bazy danych toogain hello poświadczeń hasła.

Najlepsze rozwiązania dotyczące zadania elastycznej bazy danych obejmują:

* Ogranicz użycie hello interfejsów API tootrusted osób.
* Poświadczenia powinny mieć hello co najmniej zadanie hello tooperform niezbędne uprawnienia.  Więcej informacji, można wyświetlić w ramach tego [autoryzacji i uprawnienia](https://msdn.microsoft.com/library/bb669084.aspx) artykuł w witrynie MSDN programu SQL Server.

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a>toocreate zaszyfrowane poświadczenia do wykonywania zadań dla baz danych
toocreate nową szyfrowane poświadczeń, hello [ **polecenia cmdlet Get-Credential** ](https://technet.microsoft.com/library/hh849815.aspx) monit o podanie nazwy użytkownika i hasło, które mogą zostać przekazane toohello [ **AzureSqlJobCredential nowy polecenia cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a>poświadczenia tooupdate
Po zmianie hasła, należy użyć hello [ **polecenia cmdlet Set-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) i zestaw hello **CredentialName** parametru.

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a>toodefine obiektu docelowego mapy niezależnego fragmentu elastycznej bazy danych
tooexecute zadania dla wszystkich baz danych w zestawie niezależnego fragmentu (utworzone za pomocą [biblioteki klienta elastycznej bazy danych](sql-database-elastic-database-client-library.md)), użyj mapy niezależnego fragmentu jako hello docelowej bazy danych. W tym przykładzie wymaga podzielonej aplikacji utworzony za pomocą biblioteki klienta elastycznej bazy danych hello. Zobacz [wprowadzenie próbki narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).

Hello niezależnego fragmentu Mapa menedżera z bazy danych musi być ustawiona jako docelowej bazy danych, a opcja hello mapy określonych niezależnego fragmentu musi być określona jako miejsce docelowe.

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a>Tworzenie skryptu T-SQL do wykonania dla baz danych
Podczas tworzenia skryptów T-SQL do wykonania, zdecydowanie zaleca się toobuild je toobe [idempotentności](https://en.wikipedia.org/wiki/Idempotence) i odporne na błędy. Zadania elastyczne bazy danych ponowi wykonanie skryptu zawsze, gdy wykonanie napotka błąd, niezależnie od klasyfikacji hello hello awarii.

Użyj hello [ **polecenia cmdlet New-AzureSqlJobContent** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate i zapisać skrypt do wykonania i ustaw hello **- ContentName** i **- CommandText**parametrów.

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a>Utwórz nowy skrypt z pliku
Jeśli hello skryptu T-SQL jest zdefiniowany w pliku, należy użyć tego skryptu hello tooimport:

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a>skrypt tooupdate T-SQL do wykonania dla baz danych
Tej aktualizacji skrypt programu PowerShell hello tekst polecenia T-SQL dla istniejącego skryptu.

Następujące zmienne tooreflect hello hello zestaw żądaną zestaw toobe definicji skryptu:

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a>tooupdate hello definicji tooan istniejącego skryptu
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a>toocreate tooexecute zadania skryptu w mapie niezależnego fragmentu
Ten skrypt programu PowerShell uruchamia zadania do wykonania skryptu w każdej niezależnego fragmentu w mapie niezależnego fragmentu elastycznego skalowania.

Następujące zmienne tooreflect hello hello zestaw żądaną skryptu i obiekt docelowy:

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a>tooexecute zadania
Ten skrypt programu PowerShell jest wykonywany istniejącego zadania:

Aktualizacja hello następującej zmiennej tooreflect hello żądanego zadania nazwa toohave wykonane:

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a>Stan hello tooretrieve wykonywania pojedyncze zadanie
Użyj hello [ **polecenia cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) i zestaw hello **JobExecutionId** parametru tooview hello stan wykonywania zadania.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

Użyj hello sam **Get-AzureSqlJobExecution** polecenia cmdlet z hello **właściwość IncludeChildren** parametru tooview hello stan wykonania zadania podrzędne, czyli hello określonym stanie dla każdego wykonywania zadania w odniesieniu do każdego celem zadania hello bazy danych.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a>Stan hello tooview między wieloma wykonania zadania
Witaj [ **polecenia cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) ma wiele parametrów opcjonalnych, które mogą być używane toodisplay wielu wykonania zadania, filtrowane przez hello podane parametry. Hello poniżej przedstawiono niektóre hello możliwości toouse Get-AzureSqlJobExecution:

Pobierz wszystkie aktywne najwyższego poziomu zadanie wykonaniami:

    Get-AzureSqlJobExecution

Pobierz wszystkie wykonaniami najwyższego poziomu zadania, w tym wykonaniami nieaktywnego zadania:

    Get-AzureSqlJobExecution -IncludeInactive

Pobierz wszystkie wykonania zadania podrzędne identyfikatora wykonywania podane zadanie wykonaniami nieaktywnego zadania w tym:

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

Pobierz wszystkie wykonania zadania utworzone za pomocą harmonogramu / zadania kombinacji, w tym nieaktywnych zadań:

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

Pobieranie wszystkich zadań przeznaczonych dla określonej niezależnych mapy, w tym nieaktywnych zadań:

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

Pobieranie wszystkich zadań przeznaczonych dla określonej kolekcji niestandardowych, łącznie z nieaktywnych zadań:

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

Pobrać listy hello zadanie wykonania zadania w ramach wykonania określonego zadania:

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

Pobieranie szczegółów wykonywania zadań zadania:

Witaj następującego skryptu programu PowerShell może być używane tooview hello szczegóły zadania wykonywania zadań, które jest szczególnie przydatne w przypadku debugowania awarii wykonywania.

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a>wykonania zadań tooretrieve błędów w ramach zadania
Witaj **obiektu JobTaskExecution** zawiera właściwość dla cyklu życia hello zadania hello wraz z właściwością wiadomości. Jeśli wykonanie zadania zadania nie powiodło się, będzie można ustawić właściwości cyklu życia hello zbyt** i zostanie ustawiona właściwość wiadomości powitania toohello Wynikowy komunikat o wyjątku i jego stosu. Jeśli zadanie nie powiodło się, jest ważne tooview hello szczegóły zadania, których nie powiodła się dla danego zadania.

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a>toowait dla toocomplete wykonania zadania
Hello następującego skryptu programu PowerShell może być używane toowait dla toocomplete zadań zadania:

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

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

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a>Aktualizacja zasad wykonywania niestandardowych
Aktualizacja hello potrzeby tooupdate zasad wykonywania:

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a>Anulowanie zadania
Zadania elastyczne bazy danych obsługuje żądania anulowania zadań.  Jeśli zadania elastyczne bazy danych wykryje żądanie anulowania aktualnie wykonywanego zadania, podejmie toostop hello zadania.

Istnieją dwa różne sposoby, że zadania elastyczne bazy danych można wykonać anulowania:

1. Anuluj aktualnie wykonywanych zadań: wykrycie anulowania aktualnie uruchomionej zadania anulowania będą podejmowane w hello aktualnie wykonywanych aspekt hello zadań.  Na przykład: w przypadku długo działające kwerendy obecnie wykonywana jest próba anulowania, nastąpi próba toocancel hello zapytania.
2. Anulowanie zadań ponownych prób: w przypadku anulowania wykrycia przez wątek kontroli hello przed uruchomieniu zadania do wykonania, wątek kontroli hello będzie uniknąć uruchamiania zadań hello i zadeklarować żądania hello jak anulowane.

Jeśli żądanie anulowania zadań dla zadania nadrzędnego, żądanie anulowania hello będą honorowane dla zadania nadrzędnego hello i wszystkich jego zadań podrzędnych.

toosubmit żądanie anulowania, użyj hello [ **polecenie cmdlet Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) i zestaw hello **JobExecutionId** parametru.

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a>toodelete zadania i Historia zadania asynchronicznego
Zadania elastyczne bazy danych obsługuje asynchroniczne usuwania. Zadanie może być oznaczony do usunięcia, a hello system spowoduje usunięcie hello zadania i jego historii zadań po zakończeniu wszystkich zadań wykonaniami hello zadania. Witaj systemu nie będzie automatycznie anulowania wykonaniami aktywnego zadania.  

Wywołanie [ **Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel wykonaniami aktywnego zadania.

Usuwanie zadania tootrigger, użyj hello [ **polecenia cmdlet Remove-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) i zestaw hello **JobName** parametru.

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a>toocreate obiektu docelowego w niestandardowej bazie danych
Można określić cele w niestandardowej bazie danych bezpośrednie wykonywanie lub dołączania w ramach grupy niestandardowej bazie danych. Na przykład ponieważ **pule elastyczne** są nie jest jeszcze bezpośrednio obsługiwane przy użyciu interfejsów API środowiska PowerShell, można utworzyć obiekt docelowy w niestandardowej bazie danych oraz miejsca docelowego do kolekcji niestandardowej bazy danych, które obejmuje wszystkie hello bazy danych w puli hello.

Ustaw hello następujące zmienne tooreflect hello potrzeby bazy danych:

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a>toocreate docelowej kolekcji niestandardowej bazy danych
Użyj hello [ **AzureSqlJobTarget nowy** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) toodefine polecenia cmdlet w niestandardowej bazie danych kolekcji docelowej tooenable wykonywania przez wiele obiektów docelowych określonych w bazie danych. Po utworzeniu grupy bazy danych może być skojarzony z docelowym kolekcji niestandardowej hello baz danych.

Ustaw powitania po konfiguracji docelowej żądanej kolekcji niestandardowych zmiennych tooreflect hello:

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a>tooadd baz danych tooa w niestandardowej bazie danych kolekcji docelowej
tooadd bazy danych tooa określonej kolekcji niestandardowych Użyj hello [ **AzureSqlJobChildTarget Dodaj** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) polecenia cmdlet.

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a>Przejrzyj hello bazy danych, w docelowej kolekcji niestandardowej bazy danych
Użyj hello [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) polecenia cmdlet tooretrieve hello podrzędnej bazy danych, w docelowej kolekcji niestandardowej bazie danych. 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a>Utwórz skrypt tooexecute zadania w docelowej kolekcji niestandardowej bazy danych
Użyj hello [ **AzureSqlJob nowy** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) toocreate polecenia cmdlet zadania przed grupę baz danych, wynika z docelowej kolekcji niestandardowej bazie danych. Zadania elastyczne bazy danych będzie rozszerzać hello zadania do wielu zadań podrzędnych każdego odpowiednia baza danych tooa skojarzone z hello w niestandardowej bazie danych kolekcji docelowych i upewnij się, że hello skrypt zostanie wykonany w każdej bazie danych. Ponownie ważne jest, że skrypty są odporne tooretries toobe idempotentności.

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a>Zbieranie danych dla baz danych
Można użyć zadania tooexecute kwerendy między grupą baz danych i wysyłania hello wyniki tooa określonej tabeli. Witaj tabeli może być badana po hello fakt toosee hello wyniki zapytania w każdej bazie danych. Zapewnia metody asynchronicznej tooexecute kwerendy przez wiele baz danych. Nieudanych prób są obsługiwane automatycznie za pomocą ponownych prób.

Hello określonej lokalizacji docelowej tabeli zostaną utworzone automatycznie, jeśli jeszcze nie istnieje. nową tabelę Hello zgodny schemat hello hello zwrócił zestaw wyników. Jeśli skrypt zwraca wiele zestawów wyników, zadania elastycznej bazy danych wysyła hello pierwszy toohello tabeli docelowej.

Witaj następujący skrypt programu PowerShell wykonuje skrypt i zbiera jej wyników do określonej tabeli. Ten skrypt zakłada, że skryptu T-SQL została utworzona który wyprowadza pojedynczy zestaw wyników i utworzono element docelowy kolekcji niestandardowej bazie danych.

Ten skrypt używa hello [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) polecenia cmdlet. Ustawianie parametrów hello skryptu, poświadczeń i wykonywanie obiekt docelowy:

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

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a>toocreate, a następnie Rozpocznij zadania dla scenariuszy zbierania danych
Ten skrypt używa hello [ **Start AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) polecenia cmdlet.

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a>tooschedule wyzwalacz wykonania zadania
Witaj następującego skryptu programu PowerShell może być używane toocreate za pomocą harmonogramu cyklicznego. Ten skrypt używa przedział minuty, ale [ **AzureSqlJobSchedule nowy** ](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) obsługuje również parametry - DayInterval, - HourInterval i - MonthInterval, - WeekInterval. Można utworzyć harmonogramy, które są wykonywane tylko raz przekazywanie przez - jednorazowe.

Utwórz nowy harmonogram:

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a>tootrigger zadania wykonywane zgodnie z harmonogramem czasu
Wyzwalacz zadania mogą być zdefiniowane toohave zgodnie z zadania wykonywane harmonogram tooa. Witaj następującego skryptu programu PowerShell może być używane toocreate wyzwalacza zadania.

Użyj [AzureSqlJobTrigger nowy](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) i zestaw hello następujące zmienne toocorrespond toohello żądanego zadania i harmonogramu:

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a>tooremove skojarzenia zaplanowane zadanie toostop wykonywanie zgodnie z harmonogramem
można usunąć toodiscontinue pojawiał wykonywania zadań za pomocą wyzwalacza zadania hello wyzwalacza zadania. Usuwanie zadania toostop wyzwalacz zadania wykonywane zgodnie z harmonogramem tooa przy użyciu hello [ **polecenia cmdlet Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a>Pobieranie zadania wyzwalaczy tooa powiązania harmonogramu
Witaj następującego skryptu programu PowerShell można tooobtain używane i wyświetlić hello zadania wyzwalaczy zarejestrowanych tooa określonego harmonogramu.

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a>powiązane tooa wyzwalaczy zadanie tooretrieve
Użyj [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain i wyświetlić harmonogramy zawierający zarejestrowanych zadania.

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a>toocreate aplikacji warstwy danych (DACPAC) do wykonania dla baz danych
Zobacz toocreate DACPAC [aplikacji warstwy danych](https://msdn.microsoft.com/library/ee210546.aspx). toodeploy DACPAC, użyj hello [polecenia cmdlet New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent). Witaj DACPAC musi być dostępny toohello usługi. Jest zalecana tooupload utworzony tooAzure DACPAC magazynu i Utwórz [sygnatura dostępu współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md) dla hello DACPAC.

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a>tooupdate aplikacji warstwy danych (DACPAC) do wykonania dla baz danych
Istniejące DACPACs zarejestrowanych w ramach zadania elastyczne bazy danych może być toonew toopoint zaktualizowanych identyfikatorów URI. Użyj hello [ **polecenia cmdlet Set-AzureSqlJobContentDefinition** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI na istniejącym zarejestrowany DACPAC:

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a>toocreate tooapply zadania aplikacji warstwy danych (DACPAC) dla baz danych
Po utworzeniu DACPAC w ramach zadania elastyczne bazy danych, zadania mogą być tworzone tooapply hello DACPAC między grupą baz danych. Hello następującego skryptu programu PowerShell może być używane toocreate zadania DACPAC przez niestandardowy zbiór baz danych:

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
