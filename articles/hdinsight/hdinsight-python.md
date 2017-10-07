---
title: aaaPython UDF Apache Hive i Pig - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse Python użytkownika określone funkcje (UDF) z Hive i Pig w usłudze HDInsight, hello technologii Hadoop stosu na platformie Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c44d6606-28cd-429b-b535-235e8f34a664
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/17/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 26d8160cc6ed7fc22c3f06f7c1c9954c224b2366
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a>Funkcje (UDF) za pomocą technologii Hive i Pig zdefiniowane przez użytkownika Python użycia w usłudze HDInsight

Dowiedz się, jak toouse Python zdefiniowane przez użytkownika (UDF) funkcje za pomocą Apache Hive i Pig na platformie Hadoop w usłudze Azure HDInsight.

## <a name="python"></a>Python w usłudze HDInsight

Python2.7 jest instalowany domyślnie na HDInsight 3.0 i nowszych. Apache Hive można użyć z tą wersją języka Python dla przetwarzania strumienia. Przetwarzanie strumienia używa STDOUT i STDIN danych toopass między Hive i hello funkcji zdefiniowanej przez użytkownika.

HDInsight obejmuje również Jython, który jest implementacją języka Python, napisany w języku Java. Jython działa bezpośrednio na powitania maszyny wirtualnej Java i nie używa przesyłania strumieniowego. Jython jest hello zalecane interpreter języka Python, korzystając z języka Pig języka Python.

> [!WARNING]
> kroki Hello w tym dokumencie upewnij hello następujące założenia: 
>
> * Witaj można utworzyć skrypty języka Python na środowiska deweloperskiego lokalnego.
> * Przekaż tooHDInsight skrypty hello przy użyciu albo hello `scp` polecenie sesji Bash lokalnej lub hello podany skrypt programu PowerShell.
>
> Jeśli chcesz, aby toouse hello [powłoki chmury Azure (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) Podgląd toowork z usługą HDInsight, a następnie należy:
>
> * Tworzenie skryptów hello w środowisku powłoki hello chmury.
> * Użyj `scp` tooupload hello plików z hello chmury tooHDInsight powłoki.
> * Użyj `ssh` z tooHDInsight tooconnect powłoki hello w chmurze i przykłady hello wykonywania.

## <a name="hivepython"></a>Hive funkcji zdefiniowanej przez użytkownika

Python mogą być używane jako UDF z Hive za pośrednictwem hello HiveQL `TRANSFORM` instrukcji. Na przykład po HiveQL hello wywołuje hello `hiveudf.py` plików przechowywanych w hello domyślne konto magazynu Azure hello klastra.

**HDInsight opartych na systemie Linux**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

**HDInsight opartych na systemie Windows**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> W klastrach HDInsight opartych na systemie Windows hello `USING` klauzula musi określać hello toopython.exe pełną ścieżkę.

Oto, co oznacza w tym przykładzie:

1. Witaj `add file` instrukcji na początku hello pliku hello dodaje hello `hiveudf.py` toohello pliku rozproszonej pamięci podręcznej, więc nie jest dostępny przez wszystkie węzły w klastrze hello.
2. Witaj `SELECT TRANSFORM ... USING` instrukcja wybiera danych z hello `hivesampletable`. Przekazuje ono również hello clientid, devicemake i toohello wartości devicemodel `hiveudf.py` skryptu.
3. Witaj `AS` klauzuli opisuje pola hello zwrócony z `hiveudf.py`.

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a>Utwórz plik hiveudf.py hello


Na środowiska deweloperskiego, Utwórz plik tekstowy o nazwie `hiveudf.py`. Użyj następującego kodu jako hello zawartość pliku hello hello:

```python
#!/usr/bin/env python
import sys
import string
import hashlib

while True:
    line = sys.stdin.readline()
    if not line:
        break

    line = string.strip(line, "\n ")
    clientid, devicemake, devicemodel = string.split(line, "\t")
    phone_label = devicemake + ' ' + devicemodel
    print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])
```

Ten skrypt wykonuje hello następujące akcje:

1. Odczytaj wiersz danych stdin.
2. Witaj, kończyć się znakiem nowego wiersza zostanie usunięty, za pomocą `string.strip(line, "\n ")`.
3. Podczas przetwarzania strumienia, pojedynczy wiersz zawiera wszystkich wartości hello z znak tabulacji od każdej wartości. Dlatego `string.split(line, "\t")` mogą być używane toosplit hello danych wejściowych na każdej karcie zwracanie tylko pola hello.
4. Po zakończeniu przetwarzania danych wyjściowych hello musi być napisana tooSTDOUT jako pojedynczy wiersz z kartą między każdego pola. Na przykład `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.
5. Witaj `while` pętli jest powtarzany do momentu nie `line` jest do odczytu.

dane wyjściowe skryptu Hello jest złączeniem hello wartości wejściowe dla `devicemake` i `devicemodel`, oraz skrót hello połączonych wartości.

Zobacz [uruchamianie przykładów hello](#running) jak toorun w tym przykładzie w klastrze usługi HDInsight.

## <a name="pigpython"></a>Pig funkcji zdefiniowanej przez użytkownika

Skrypt w języku Python może służyć jako UDF z Pig za pośrednictwem hello `GENERATE` instrukcji. Można uruchomić skryptu hello za pomocą Jython lub C Python.

* Jython działa na powitania JVM i natywnie można wywołać z Pig.
* C Python to proces zewnętrzny, więc dane hello z Pig na powitania JVM wysłaniu toohello skrypt uruchomiony w procesie Python. dane wyjściowe Hello hello skrypt w języku Python są wysyłane do Pig.

interpreter języka Python hello toospecify, użyj `register` podczas odwoływania się do hello skrypt w języku Python. Witaj następujące przykłady Zarejestruj skrypty Pig jako `myfuncs`:

* **toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`
* **toouse C Python**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`

> [!IMPORTANT]
> Podczas korzystania z Jython, hello ścieżki toohello pig_jython pliku może być ścieżką lokalną lub WASB: / / ścieżki. Jednak podczas korzystania z języka Python C, możesz odwoływać pliku w systemie pliku lokalnego hello węzła hello używasz zadania programu Pig hello toosubmit.

Po poza rejestracji hello Pig Latin w tym przykładzie hello sam zarówno dla:

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

Oto, co oznacza w tym przykładzie:

1. pierwszy wiersz Hello ładuje hello przykładowy plik danych `sample.log` do `LOGS`. Definiuje również każdego rekordu jako `chararray`.
2. następnego wiersza Hello odfiltrowuje wszystkie wartości null, hello wynik operacji hello do przechowywania `LOG`.
3. Następnie iteruje za pośrednictwem hello rekordów w `LOG` i używa `GENERATE` tooinvoke hello `create_structure` metody zawarte w skrypcie Python/Jython hello załadowany jako `myfuncs`. `LINE`jest używana toopass hello bieżącej funkcji toohello rekordów.
4. Ponadto dane wyjściowe hello są zrzut tooSTDOUT przy użyciu hello `DUMP` polecenia. To polecenie wyświetla wyniki powitania po zakończeniu operacji hello.

### <a name="create-hello-pigudfpy-file"></a>Utwórz plik pigudf.py hello

Na środowiska deweloperskiego, Utwórz plik tekstowy o nazwie `pigudf.py`. Użyj następującego kodu jako hello zawartość pliku hello hello:

<a name="streamingpy"></a>

```python
# Uncomment hello following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

Przykład Witaj Pig Latin zdefiniowanego hello `LINE` danych wejściowych jako chararray, ponieważ nie istnieje zgodny schematu dla danych wejściowych hello. Witaj skrypt w języku Python przekształca hello danych w spójne schematu dla danych wyjściowych.

1. Witaj `@outputSchema` hello format danych zwracanych tooPig hello definiuje instrukcji. W takim przypadku ma **pakiet danych**, który jest typem danych Pig. Witaj w zbiorze zawiera hello kolejnych pól, które są chararray (ciągi):

   * Data — Witaj wpis dziennika hello Data utworzenia
   * raz — Witaj hello wpis dziennika został utworzony.
   * klasy — Witaj klasy nazwa hello zapis został utworzony dla
   * poziom — Witaj poziom dziennika
   * Szczegóły — pełne szczegóły hello wpis dziennika.

2. Następnie hello `def create_structure(input)` definiuje funkcję hello, Pig przekazujący pozycji do.

3. Witaj przykładowe dane `sample.log`, przede wszystkim zgodne toohello dzień, godzina classname poziomu i szczegółów chcemy tooreturn schematu. Jednak zawiera kilka wierszy, które zaczynają się od `*java.lang.Exception*`. Te wiersze musi być zmodyfikowany toomatch hello schematu. Witaj `if` instrukcji wyszukuje, a następnie masażystów hello hello toomove danych wejściowych `*java.lang.Exception*` celu toohello ciąg dostarczają hello danych w linii z naszych schematu oczekiwane dane wyjściowe.

4. Następnie hello `split` polecenia jest używane toosplit hello danych na powitania pierwsze cztery miejsca znaków. dane wyjściowe Hello jest przypisany do `date`, `time`, `classname`, `level`, i `detail`.

5. Na koniec hello wartości są zwracane tooPig.

Po zwróceniu danych hello tooPig, ma schemat spójny, zgodnie z definicją w hello `@outputSchema` instrukcji.

## <a name="running"></a>Przekaż, a następnie uruchom hello przykłady

> [!IMPORTANT]
> Witaj **SSH** kroki pracować tylko z klastra usługi HDInsight opartej na systemie Linux. Witaj **PowerShell** kroki pracy z klastra z systemem Linux lub HDInsight opartych na systemie Windows, ale wymaga klienta systemu Windows.

### <a name="ssh"></a>SSH

Aby uzyskać więcej informacji o korzystaniu z protokołu SSH, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

1. Użyj `scp` klastra usługi HDInsight tooyour toocopy hello plików. Na przykład Witaj następujące polecenia kopie hello pliki tooa klastra o nazwie **mycluster**.

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. Używanie protokołu SSH tooconnect toohello klastra.

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. W sesji SSH hello dodanie plików python hello wcześniej przekazany toohello WASB magazyn dla klastra hello.

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

Po przekazaniu plików hello, użyj następujących hello kroki toorun hello Hive i Pig zadania.

#### <a name="use-hello-hive-udf"></a>Użyj hello Hive funkcji zdefiniowanej przez użytkownika

1. Użyj hello `hive` toostart hello hive powłoki poleceń. Powinny pojawić się `hive>` Monituj po załadowaniu hello powłoki.

2. Wprowadź hello następującego zapytania na powitania `hive>` wiersza:

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. Po wprowadzeniu hello ostatni wiersz, należy zacząć hello zadania. Po zakończeniu zadania hello zwraca dane wyjściowe toohello podobnie poniższy przykład:

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a>Użyj hello Pig UDF

1. Użyj hello `pig` toostart hello powłoki poleceń. Zostanie wyświetlony `grunt>` Monituj po załadowaniu hello powłoki.

2. Wprowadź następujące instrukcje na powitania hello `grunt>` wiersza:

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. Po wprowadzeniu hello następującego wiersza, należy zacząć hello zadania. Po zakończeniu zadania hello zwraca dane wyjściowe toohello podobne następujące dane:

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. Użyj `quit` tooexit hello Grunt powłoki, a następnie użyj hello poniższe tooedit hello pigudf.py plik na powitania lokalnego systemu plików:

    ```bash
    nano pigudf.py
    ```

5. Raz w edytorze hello, usuń znaczniki komentarza powitania po wierszu przez usunięcie hello `#` znaku od początku hello hello wiersza:

    ```bash
    #from pig_util import outputSchema
    ```

    Po hello zmiany zostały wprowadzone, należy użyć edytora hello tooexit Ctrl + X. Wybierz Y, a następnie wprowadź zmiany hello toosave.

6. Użyj hello `pig` polecenia powłoki hello toostart ponownie. Po przejściu na powitania `grunt>` monit, użyj następującego skryptu Python hello toorun za pomocą interpreter języka Python C hello hello.

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    Po zakończeniu tego zadania, co za wcześniej hello skryptu za pomocą Jython powinna zostać wyświetlona hello sam wyjściowy.

### <a name="powershell-upload-hello-files"></a>Środowiska PowerShell: Pliki hello przekazywania

Można użyć programu PowerShell tooupload hello plików toohello HDInsight serwera. Użyj hello następujące pliki Python hello tooupload skryptu:

> [!IMPORTANT] 
> kroki Hello w tej sekcji, użyj programu Azure PowerShell. Aby uzyskać więcej informacji na temat używania programu Azure PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
# Change hello path toomatch hello file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

Set-AzureStorageBlobContent `
    -File $pathToStreamingFile `
    -Blob "hiveudf.py" `
    -Container $container `
    -Context $context

Set-AzureStorageBlobContent `
    -File $pathToJythonFile `
    -Blob "pigudf.py" `
    -Container $container `
    -Context $context
```
> [!IMPORTANT]
> Zmień hello `C:\path\to` wartość toohello ścieżka toohello plików na środowiska deweloperskiego.

Ten skrypt powoduje pobranie informacji o dla klastra usługi HDInsight, a następnie wyodrębnia hello konta i klucz dla hello domyślne konto magazynu i przekazywanie hello głównego toohello pliki hello kontenera.

> [!NOTE]
> Aby uzyskać więcej informacji dotyczących przekazywania plików, zobacz hello [przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight](hdinsight-upload-data.md) dokumentu.

#### <a name="powershell-use-hello-hive-udf"></a>Programu PowerShell: Hello Hive UDF Użyj

PowerShell może być również używane tooremotely uruchamiania zapytań Hive. Użyj powitania po toorun skrypt programu PowerShell zapytań programu Hive, która używa **hiveudf.py** skryptu:

> [!IMPORTANT]
> Przed uruchomieniem, skrypt hello monituje o hello HTTPs/Admin informacje o koncie dla klastra usługi HDInsight.

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

# If using a Windows-based HDInsight cluster, change hello USING statement to:
# "USING 'D:\Python27\python.exe hiveudf.py' AS " +
$HiveQuery = "add file wasb:///hiveudf.py;" +
                "SELECT TRANSFORM (clientid, devicemake, devicemodel) " +
                "USING 'python hiveudf.py' AS " +
                "(clientid string, phoneLabel string, phoneHash string) " +
                "FROM hivesampletable " +
                "ORDER BY clientid LIMIT 50;"

$jobDefinition = New-AzureRmHDInsightHiveJobDefinition `
    -Query $HiveQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds
Write-Host "Wait for hello Hive job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

Witaj danych wyjściowych dla hello **Hive** zadania powinien zostać wyświetlony toohello podobnie poniższy przykład:

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a>Pig (Jython)

PowerShell może być również używane toorun Pig Latin zadania. toorun zadania Pig Latin, który używa hello **pigudf.py** skryptu, użyj następującego skryptu programu PowerShell hello:

> [!NOTE]
> Gdy zdalne przesyłania zadania przy użyciu programu PowerShell, nie jest możliwe toouse C Python jako hello interpreter.

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

$PigQuery = "Register wasb:///pigudf.py using jython as myfuncs;" +
            "LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);" +
            "LOG = FILTER LOGS by LINE is not null;" +
            "DETAILS = foreach LOG generate myfuncs.create_structure(LINE);" +
            "DUMP DETAILS;"

$jobDefinition = New-AzureRmHDInsightPigJobDefinition -Query $PigQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds

Write-Host "Wait for hello Pig job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

Witaj danych wyjściowych dla hello **Pig** zadania powinien zostać wyświetlony podobne toohello następujące dane:

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <a name="troubleshooting"></a>Rozwiązywanie problemów

### <a name="errors-when-running-jobs"></a>Błędy podczas uruchamiania zadania

Podczas uruchamiania zadania hive hello, może wystąpić błąd podobny toohello następującego tekstu:

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

Ten problem może być spowodowane hello zakończenia wierszy w pliku języka Python hello. Wiele edytorów Windows domyślne toousing CRLF jako wiersz hello zakończenia, ale zwykle LF aplikacje w systemie Linux.

Program hello następujące znaki hello CR tooremove instrukcje PowerShell przed przekazaniem tooHDInsight pliku hello:

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a>Skrypty programu PowerShell

Przykładu hello skryptów programu PowerShell używanych toorun hello przykłady zawierają komentarze wiersza, który wyświetla dane wyjściowe błędów hello zadania. Jeśli nie widzisz hello oczekuje danych wyjściowych zadania hello, usuń znaczniki komentarza hello następujący wiersz i zobacz, czy informacje o błędzie hello wskazuje na problem.

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

informacje o błędzie Hello (STDERR) oraz hello wyniku zadania hello (STDOUT) są również zarejestrowane tooyour magazynu usługi HDInsight.

| Dla tego zadania... | Przyjrzyj się te pliki w kontenerze obiektów blob hello |
| --- | --- |
| Hive |/ HivePython/stderr<p>/ HivePython/stdout |
| Pig |/ PigPython/stderr<p>/ PigPython/stdout |

## <a name="next"></a>Następne kroki

Jeśli potrzebujesz tooload modułów środowiska Python, które domyślnie nie są dostępne, zobacz [jak toodeploy tooAzure modułu HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).

Inne sposoby toouse Pig, Hive i toolearn o korzystaniu z MapReduce Zobacz hello w następujących dokumentach:

* [Korzystanie z programu Hive z usługą HDInsight](hdinsight-use-hive.md)
* [Korzystanie z języka Pig z usługą HDInsight](hdinsight-use-pig.md)
* [Korzystać z usługi MapReduce z usługą HDInsight](hdinsight-use-mapreduce.md)
