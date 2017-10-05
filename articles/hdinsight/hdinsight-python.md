---
title: "Python funkcji zdefiniowanej przez użytkownika z Apache Hive i wieprzowa — usługa Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać języka Python użytkownika określone funkcje (UDF) z Hive i Pig w usłudze HDInsight Hadoop stosu technologii na platformie Azure."
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
ms.openlocfilehash: 9b67ded05a52f1e68580434667495cf6cf939871
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="43126-103">Funkcje (UDF) za pomocą technologii Hive i Pig zdefiniowane przez użytkownika Python użycia w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="43126-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="43126-104">Dowiedz się, jak używać języka Python funkcje zdefiniowane przez użytkownika (UDF) z Apache Hive i Pig na platformie Hadoop w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="43126-104">Learn how to use Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="43126-105"><a name="python"></a>Python w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="43126-105"><a name="python"></a>Python on HDInsight</span></span>

<span data-ttu-id="43126-106">Python2.7 jest instalowany domyślnie na HDInsight 3.0 i nowszych.</span><span class="sxs-lookup"><span data-stu-id="43126-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span></span> <span data-ttu-id="43126-107">Apache Hive można użyć z tą wersją języka Python dla przetwarzania strumienia.</span><span class="sxs-lookup"><span data-stu-id="43126-107">Apache Hive can be used with this version of Python for stream processing.</span></span> <span data-ttu-id="43126-108">Przetwarzanie strumienia używa STDOUT i STDIN do przekazywania danych między Hive i funkcję zdefiniowaną przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="43126-108">Stream processing uses STDOUT and STDIN to pass data between Hive and the UDF.</span></span>

<span data-ttu-id="43126-109">HDInsight obejmuje również Jython, który jest implementacją języka Python, napisany w języku Java.</span><span class="sxs-lookup"><span data-stu-id="43126-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="43126-110">Jython działa bezpośrednio na maszynie wirtualnej Java i nie używa przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="43126-110">Jython runs directly on the Java Virtual Machine and does not use streaming.</span></span> <span data-ttu-id="43126-111">Jython jest zalecane interpreter języka Python, korzystając z języka Python z języka Pig.</span><span class="sxs-lookup"><span data-stu-id="43126-111">Jython is the recommended Python interpreter when using Python with Pig.</span></span>

> [!WARNING]
> <span data-ttu-id="43126-112">Kroki opisane w tym dokumencie mieć następujące wartości domyślne:</span><span class="sxs-lookup"><span data-stu-id="43126-112">The steps in this document make the following assumptions:</span></span> 
>
> * <span data-ttu-id="43126-113">Można utworzyć skrypty języka Python na środowiska deweloperskiego lokalnego.</span><span class="sxs-lookup"><span data-stu-id="43126-113">You create the Python scripts on your local development environment.</span></span>
> * <span data-ttu-id="43126-114">Możesz przekazać do usługi HDInsight przy użyciu skryptów `scp` polecenie sesję Bash lokalnego lub udostępnionego skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="43126-114">You upload the scripts to HDInsight using either the `scp` command from a local Bash session or the provided PowerShell script.</span></span>
>
> <span data-ttu-id="43126-115">Jeśli chcesz użyć [powłoki chmury Azure (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) Podgląd, aby pracować z usługą HDInsight, a następnie należy:</span><span class="sxs-lookup"><span data-stu-id="43126-115">If you want to use the [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview to work with HDInsight, then you must:</span></span>
>
> * <span data-ttu-id="43126-116">Tworzenie skryptów w środowisku chmury powłoki.</span><span class="sxs-lookup"><span data-stu-id="43126-116">Create the scripts inside the cloud shell environment.</span></span>
> * <span data-ttu-id="43126-117">Użyj `scp` przekazywania plików z poziomu powłoki chmury do usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="43126-117">Use `scp` to upload the files from the cloud shell to HDInsight.</span></span>
> * <span data-ttu-id="43126-118">Użyj `ssh` z poziomu powłoki chmury, aby podłączyć się do usługi HDInsight i uruchamiania przykładów.</span><span class="sxs-lookup"><span data-stu-id="43126-118">Use `ssh` from the cloud shell to connect to HDInsight and run the examples.</span></span>

## <span data-ttu-id="43126-119"><a name="hivepython"></a>Hive funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="43126-119"><a name="hivepython"></a>Hive UDF</span></span>

<span data-ttu-id="43126-120">Python, mogą być używane jako UDF z Hive za pośrednictwem HiveQL `TRANSFORM` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="43126-120">Python can be used as a UDF from Hive through the HiveQL `TRANSFORM` statement.</span></span> <span data-ttu-id="43126-121">Na przykład następujące HiveQL wywołuje `hiveudf.py` plików przechowywanych w domyślne konto magazynu Azure dla klastra.</span><span class="sxs-lookup"><span data-stu-id="43126-121">For example, the following HiveQL invokes the `hiveudf.py` file stored in the default Azure Storage account for the cluster.</span></span>

<span data-ttu-id="43126-122">**HDInsight opartych na systemie Linux**</span><span class="sxs-lookup"><span data-stu-id="43126-122">**Linux-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="43126-123">**HDInsight opartych na systemie Windows**</span><span class="sxs-lookup"><span data-stu-id="43126-123">**Windows-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="43126-124">W klastrach HDInsight opartych na systemie Windows `USING` klauzuli należy określić pełną ścieżkę do python.exe.</span><span class="sxs-lookup"><span data-stu-id="43126-124">On Windows-based HDInsight clusters, the `USING` clause must specify the full path to python.exe.</span></span>

<span data-ttu-id="43126-125">Oto, co oznacza w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="43126-125">Here's what this example does:</span></span>

1. <span data-ttu-id="43126-126">`add file` Dodaje oświadczenie na początku pliku `hiveudf.py` plik do rozproszonej pamięci podręcznej, więc nie jest dostępny przez wszystkie węzły w klastrze.</span><span class="sxs-lookup"><span data-stu-id="43126-126">The `add file` statement at the beginning of the file adds the `hiveudf.py` file to the distributed cache, so it's accessible by all nodes in the cluster.</span></span>
2. <span data-ttu-id="43126-127">`SELECT TRANSFORM ... USING` Instrukcja wybiera dane z `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="43126-127">The `SELECT TRANSFORM ... USING` statement selects data from the `hivesampletable`.</span></span> <span data-ttu-id="43126-128">Przekazuje także wartości clientid, devicemake i devicemodel `hiveudf.py` skryptu.</span><span class="sxs-lookup"><span data-stu-id="43126-128">It also passes the clientid, devicemake, and devicemodel values to the `hiveudf.py` script.</span></span>
3. <span data-ttu-id="43126-129">`AS` Klauzuli opisano pola zwrócony z `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="43126-129">The `AS` clause describes the fields returned from `hiveudf.py`.</span></span>

<a name="streamingpy"></a>

### <a name="create-the-hiveudfpy-file"></a><span data-ttu-id="43126-130">Utwórz plik hiveudf.py</span><span class="sxs-lookup"><span data-stu-id="43126-130">Create the hiveudf.py file</span></span>


<span data-ttu-id="43126-131">Na środowiska deweloperskiego, Utwórz plik tekstowy o nazwie `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="43126-131">On your development environment, create a text file named `hiveudf.py`.</span></span> <span data-ttu-id="43126-132">Zawartość pliku, należy użyć poniższego kodu:</span><span class="sxs-lookup"><span data-stu-id="43126-132">Use the following code as the contents of the file:</span></span>

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

<span data-ttu-id="43126-133">Ten skrypt wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="43126-133">This script performs the following actions:</span></span>

1. <span data-ttu-id="43126-134">Odczytaj wiersz danych stdin.</span><span class="sxs-lookup"><span data-stu-id="43126-134">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="43126-135">Końcowy znak nowego wiersza zostanie usunięty, za pomocą `string.strip(line, "\n ")`.</span><span class="sxs-lookup"><span data-stu-id="43126-135">The trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="43126-136">W trakcie przetwarzania strumieni, pojedynczy wiersz zawiera wszystkie wartości z znak tabulacji od każdej wartości.</span><span class="sxs-lookup"><span data-stu-id="43126-136">When doing stream processing, a single line contains all the values with a tab character between each value.</span></span> <span data-ttu-id="43126-137">Dlatego `string.split(line, "\t")` można podzielić na każdej karcie zwracanie tylko pola danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="43126-137">So `string.split(line, "\t")` can be used to split the input at each tab, returning just the fields.</span></span>
4. <span data-ttu-id="43126-138">Po zakończeniu przetwarzania danych wyjściowych musi być przystosowana do STDOUT jako pojedynczy wiersz z kartą między każdego pola.</span><span class="sxs-lookup"><span data-stu-id="43126-138">When processing is complete, the output must be written to STDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="43126-139">Na przykład `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span><span class="sxs-lookup"><span data-stu-id="43126-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="43126-140">`while` Pętli jest powtarzany do momentu nie `line` jest do odczytu.</span><span class="sxs-lookup"><span data-stu-id="43126-140">The `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="43126-141">Dane wyjściowe skryptu jest złączeniem wartości wejściowe dla `devicemake` i `devicemodel`oraz skrót połączonych wartości.</span><span class="sxs-lookup"><span data-stu-id="43126-141">The script output is a concatenation of the input values for `devicemake` and `devicemodel`, and a hash of the concatenated value.</span></span>

<span data-ttu-id="43126-142">Zobacz [uruchamiania przykładów](#running) instrukcje do uruchomienia tego przykładu w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="43126-142">See [Running the examples](#running) for how to run this example on your HDInsight cluster.</span></span>

## <span data-ttu-id="43126-143"><a name="pigpython"></a>Pig funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="43126-143"><a name="pigpython"></a>Pig UDF</span></span>

<span data-ttu-id="43126-144">Skrypt w języku Python może służyć jako UDF z Pig za pośrednictwem `GENERATE` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="43126-144">A Python script can be used as a UDF from Pig through the `GENERATE` statement.</span></span> <span data-ttu-id="43126-145">Można uruchomić skryptu za pomocą Jython lub C Python.</span><span class="sxs-lookup"><span data-stu-id="43126-145">You can run the script using either Jython or C Python.</span></span>

* <span data-ttu-id="43126-146">Jython działa na JVM i natywnie można wywołać z Pig.</span><span class="sxs-lookup"><span data-stu-id="43126-146">Jython runs on the JVM, and can natively be called from Pig.</span></span>
* <span data-ttu-id="43126-147">C Python to proces zewnętrzny, dlatego dane z Pig na maszyna JVM są wysyłane do skrypt uruchomiony w procesie Python.</span><span class="sxs-lookup"><span data-stu-id="43126-147">C Python is an external process, so the data from Pig on the JVM is sent out to the script running in a Python process.</span></span> <span data-ttu-id="43126-148">Dane wyjściowe skryptu Python są wysyłane do Pig.</span><span class="sxs-lookup"><span data-stu-id="43126-148">The output of the Python script is sent back into Pig.</span></span>

<span data-ttu-id="43126-149">Aby określić interpreter języka Python, użyj `register` podczas odwoływania się do skryptu języka Python.</span><span class="sxs-lookup"><span data-stu-id="43126-149">To specify the Python interpreter, use `register` when referencing the Python script.</span></span> <span data-ttu-id="43126-150">Poniższe przykłady Zarejestruj skrypty Pig jako `myfuncs`:</span><span class="sxs-lookup"><span data-stu-id="43126-150">The following examples register scripts with Pig as `myfuncs`:</span></span>

* <span data-ttu-id="43126-151">**Aby użyć Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="43126-151">**To use Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="43126-152">**Aby użyć C Python**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="43126-152">**To use C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43126-153">Podczas korzystania z Jython, ścieżka do pliku pig_jython może być ścieżką lokalną lub WASB: / / ścieżki.</span><span class="sxs-lookup"><span data-stu-id="43126-153">When using Jython, the path to the pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="43126-154">Jednak podczas korzystania z języka Python C, możesz odwoływać pliku w systemie pliku lokalnego węzła, który używasz przesłać zadania programu Pig.</span><span class="sxs-lookup"><span data-stu-id="43126-154">However, when using C Python, you must reference a file on the local file system of the node that you are using to submit the Pig job.</span></span>

<span data-ttu-id="43126-155">Raz po rejestracji, Pig Latin w tym przykładzie jest taki sam zarówno dla:</span><span class="sxs-lookup"><span data-stu-id="43126-155">Once past registration, the Pig Latin for this example is the same for both:</span></span>

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="43126-156">Oto, co oznacza w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="43126-156">Here's what this example does:</span></span>

1. <span data-ttu-id="43126-157">Pierwszy wiersz ładuje przykładowy plik danych `sample.log` do `LOGS`.</span><span class="sxs-lookup"><span data-stu-id="43126-157">The first line loads the sample data file, `sample.log` into `LOGS`.</span></span> <span data-ttu-id="43126-158">Definiuje również każdego rekordu jako `chararray`.</span><span class="sxs-lookup"><span data-stu-id="43126-158">It also defines each record as a `chararray`.</span></span>
2. <span data-ttu-id="43126-159">Następnego wiersza odfiltrowuje wszystkie wartości null, wynik operacji do przechowywania `LOG`.</span><span class="sxs-lookup"><span data-stu-id="43126-159">The next line filters out any null values, storing the result of the operation into `LOG`.</span></span>
3. <span data-ttu-id="43126-160">Następnie przechodzi on przez rekordy w `LOG` i używa `GENERATE` do wywołania `create_structure` metody zawarte w skrypcie Python/Jython załadowany jako `myfuncs`.</span><span class="sxs-lookup"><span data-stu-id="43126-160">Next, it iterates over the records in `LOG` and uses `GENERATE` to invoke the `create_structure` method contained in the Python/Jython script loaded as `myfuncs`.</span></span> <span data-ttu-id="43126-161">`LINE`Służy do przekazania bieżącego rekordu do funkcji.</span><span class="sxs-lookup"><span data-stu-id="43126-161">`LINE` is used to pass the current record to the function.</span></span>
4. <span data-ttu-id="43126-162">Na koniec utworzyć zrzutu dane wyjściowe stdout przy użyciu `DUMP` polecenia.</span><span class="sxs-lookup"><span data-stu-id="43126-162">Finally, the outputs are dumped to STDOUT using the `DUMP` command.</span></span> <span data-ttu-id="43126-163">To polecenie wyświetla wyniki po zakończeniu operacji.</span><span class="sxs-lookup"><span data-stu-id="43126-163">This command displays the results after the operation completes.</span></span>

### <a name="create-the-pigudfpy-file"></a><span data-ttu-id="43126-164">Utwórz plik pigudf.py</span><span class="sxs-lookup"><span data-stu-id="43126-164">Create the pigudf.py file</span></span>

<span data-ttu-id="43126-165">Na środowiska deweloperskiego, Utwórz plik tekstowy o nazwie `pigudf.py`.</span><span class="sxs-lookup"><span data-stu-id="43126-165">On your development environment, create a text file named `pigudf.py`.</span></span> <span data-ttu-id="43126-166">Zawartość pliku, należy użyć poniższego kodu:</span><span class="sxs-lookup"><span data-stu-id="43126-166">Use the following code as the contents of the file:</span></span>

<a name="streamingpy"></a>

```python
# Uncomment the following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

<span data-ttu-id="43126-167">W tym przykładzie Pig Latin zdefiniowanego `LINE` danych wejściowych jako chararray, ponieważ nie istnieje zgodny schematu dla danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="43126-167">In the Pig Latin example, we defined the `LINE` input as a chararray because there is no consistent schema for the input.</span></span> <span data-ttu-id="43126-168">Skrypt w języku Python przekształca danych w spójne schematu dla danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="43126-168">The Python script transforms the data into a consistent schema for output.</span></span>

1. <span data-ttu-id="43126-169">`@outputSchema` Instrukcji definiuje format danych, która jest zwracana do Pig.</span><span class="sxs-lookup"><span data-stu-id="43126-169">The `@outputSchema` statement defines the format of the data that is returned to Pig.</span></span> <span data-ttu-id="43126-170">W takim przypadku ma **pakiet danych**, który jest typem danych Pig.</span><span class="sxs-lookup"><span data-stu-id="43126-170">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="43126-171">Zbiorze zawiera następujące pola, które są chararray (ciągi):</span><span class="sxs-lookup"><span data-stu-id="43126-171">The bag contains the following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="43126-172">Data — Data utworzenia wpisu dziennika</span><span class="sxs-lookup"><span data-stu-id="43126-172">date - the date the log entry was created</span></span>
   * <span data-ttu-id="43126-173">Czas — czas utworzenia wpisu dziennika</span><span class="sxs-lookup"><span data-stu-id="43126-173">time - the time the log entry was created</span></span>
   * <span data-ttu-id="43126-174">klasy — Nazwa klasy zapis został utworzony dla</span><span class="sxs-lookup"><span data-stu-id="43126-174">classname - the class name the entry was created for</span></span>
   * <span data-ttu-id="43126-175">poziom — poziom dziennika</span><span class="sxs-lookup"><span data-stu-id="43126-175">level - the log level</span></span>
   * <span data-ttu-id="43126-176">Szczegóły — pełne szczegóły wpisu dziennika</span><span class="sxs-lookup"><span data-stu-id="43126-176">detail - verbose details for the log entry</span></span>

2. <span data-ttu-id="43126-177">Następnie `def create_structure(input)` definiuje funkcję, która Pig przekazuje pozycji do.</span><span class="sxs-lookup"><span data-stu-id="43126-177">Next, the `def create_structure(input)` defines the function that Pig passes line items to.</span></span>

3. <span data-ttu-id="43126-178">Przykładowe dane `sample.log`, przede wszystkim odpowiada dzień, godzina classname poziomu i szczegółów schematu chcemy, aby wrócić.</span><span class="sxs-lookup"><span data-stu-id="43126-178">The example data, `sample.log`, mostly conforms to the date, time, classname, level, and detail schema we want to return.</span></span> <span data-ttu-id="43126-179">Jednak zawiera kilka wierszy, które zaczynają się od `*java.lang.Exception*`.</span><span class="sxs-lookup"><span data-stu-id="43126-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span></span> <span data-ttu-id="43126-180">Należy zmodyfikować te wiersze, aby być zgodna ze schematem.</span><span class="sxs-lookup"><span data-stu-id="43126-180">These lines must be modified to match the schema.</span></span> <span data-ttu-id="43126-181">`if` Instrukcji sprawdza, czy te, a następnie massages dane wejściowe, aby przenieść `*java.lang.Exception*` ciąg w celu wprowadzenia danych w zewnętrznych z naszych schematu oczekiwane dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="43126-181">The `if` statement checks for those, then massages the input data to move the `*java.lang.Exception*` string to the end, bringing the data in-line with our expected output schema.</span></span>

4. <span data-ttu-id="43126-182">Następnie `split` polecenie służy do dzielenia danych na pierwszy znaków czterech spacji.</span><span class="sxs-lookup"><span data-stu-id="43126-182">Next, the `split` command is used to split the data at the first four space characters.</span></span> <span data-ttu-id="43126-183">Dane wyjściowe jest przypisany do `date`, `time`, `classname`, `level`, i `detail`.</span><span class="sxs-lookup"><span data-stu-id="43126-183">The output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span></span>

5. <span data-ttu-id="43126-184">Na koniec wartości są zwracane do Pig.</span><span class="sxs-lookup"><span data-stu-id="43126-184">Finally, the values are returned to Pig.</span></span>

<span data-ttu-id="43126-185">Gdy dane są zwracane do Pig, ma schemat spójny, zgodnie z definicją w `@outputSchema` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="43126-185">When the data is returned to Pig, it has a consistent schema as defined in the `@outputSchema` statement.</span></span>

## <span data-ttu-id="43126-186"><a name="running"></a>Przekazywanie i uruchamiania przykładów</span><span class="sxs-lookup"><span data-stu-id="43126-186"><a name="running"></a>Upload and run the examples</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43126-187">**SSH** kroki pracować tylko z klastra usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="43126-187">The **SSH** steps only work with a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="43126-188">**PowerShell** kroki pracy z klastra z systemem Linux lub HDInsight opartych na systemie Windows, ale wymaga klienta systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="43126-188">The **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span></span>

### <a name="ssh"></a><span data-ttu-id="43126-189">SSH</span><span class="sxs-lookup"><span data-stu-id="43126-189">SSH</span></span>

<span data-ttu-id="43126-190">Aby uzyskać więcej informacji o korzystaniu z protokołu SSH, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="43126-190">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="43126-191">Użyj `scp` do kopiowania plików do klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="43126-191">Use `scp` to copy the files to your HDInsight cluster.</span></span> <span data-ttu-id="43126-192">Na przykład następujące polecenie kopiuje pliki do klastra o nazwie **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="43126-192">For example, the following command copies the files to a cluster named **mycluster**.</span></span>

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. <span data-ttu-id="43126-193">Używanie protokołu SSH, aby połączyć się z klastrem.</span><span class="sxs-lookup"><span data-stu-id="43126-193">Use SSH to connect to the cluster.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="43126-194">W sesji SSH należy dodać pliki python wcześniej przekazany do magazynu WASB dla klastra.</span><span class="sxs-lookup"><span data-stu-id="43126-194">From the SSH session, add the python files uploaded previously to the WASB storage for the cluster.</span></span>

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

<span data-ttu-id="43126-195">Po przekazaniu plików, wykonaj następujące kroki, aby uruchamiać zadania Hive i Pig.</span><span class="sxs-lookup"><span data-stu-id="43126-195">After uploading the files, use the following steps to run the Hive and Pig jobs.</span></span>

#### <a name="use-the-hive-udf"></a><span data-ttu-id="43126-196">Korzystanie z programu Hive funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="43126-196">Use the Hive UDF</span></span>

1. <span data-ttu-id="43126-197">Użyj `hive` polecenie, aby uruchomić powłokę programu hive.</span><span class="sxs-lookup"><span data-stu-id="43126-197">Use the `hive` command to start the hive shell.</span></span> <span data-ttu-id="43126-198">Powinny pojawić się `hive>` Monituj po załadowaniu powłoki.</span><span class="sxs-lookup"><span data-stu-id="43126-198">You should see a `hive>` prompt once the shell has loaded.</span></span>

2. <span data-ttu-id="43126-199">Wpisz poniższe zapytanie na `hive>` wiersza:</span><span class="sxs-lookup"><span data-stu-id="43126-199">Enter the following query at the `hive>` prompt:</span></span>

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. <span data-ttu-id="43126-200">Po wprowadzeniu ostatni wiersz, należy uruchomić zadanie.</span><span class="sxs-lookup"><span data-stu-id="43126-200">After entering the last line, the job should start.</span></span> <span data-ttu-id="43126-201">Po zakończeniu zadania zwraca dane wyjściowe podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="43126-201">Once the job completes, it returns output similar to the following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-the-pig-udf"></a><span data-ttu-id="43126-202">Korzystanie z języka Pig funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="43126-202">Use the Pig UDF</span></span>

1. <span data-ttu-id="43126-203">Użyj `pig` polecenie, aby uruchomić powłoki.</span><span class="sxs-lookup"><span data-stu-id="43126-203">Use the `pig` command to start the shell.</span></span> <span data-ttu-id="43126-204">Zostanie wyświetlony `grunt>` Monituj po załadowaniu powłoki.</span><span class="sxs-lookup"><span data-stu-id="43126-204">You see a `grunt>` prompt once the shell has loaded.</span></span>

2. <span data-ttu-id="43126-205">Wprowadź następujące instrukcje w `grunt>` wierszu:</span><span class="sxs-lookup"><span data-stu-id="43126-205">Enter the following statements at the `grunt>` prompt:</span></span>

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="43126-206">Po wprowadzeniu z następującego wiersza, należy uruchomić zadanie.</span><span class="sxs-lookup"><span data-stu-id="43126-206">After entering the following line, the job should start.</span></span> <span data-ttu-id="43126-207">Po zakończeniu zadania zwraca dane wyjściowe podobne do następujących danych:</span><span class="sxs-lookup"><span data-stu-id="43126-207">Once the job completes, it returns output similar to the following data:</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="43126-208">Użyj `quit` aby zakończyć powłoki Grunt, a następnie przeprowadź edycję pliku pigudf.py w lokalnym systemie plików należy wykonać następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="43126-208">Use `quit` to exit the Grunt shell, and then use the following to edit the pigudf.py file on the local file system:</span></span>

    ```bash
    nano pigudf.py
    ```

5. <span data-ttu-id="43126-209">Raz w edytorze, usuń znaczniki komentarza następujący wiersz przez usunięcie `#` znaku od początku wiersza:</span><span class="sxs-lookup"><span data-stu-id="43126-209">Once in the editor, uncomment the following line by removing the `#` character from the beginning of the line:</span></span>

    ```bash
    #from pig_util import outputSchema
    ```

    <span data-ttu-id="43126-210">Po dokonaniu zmian, użyj klawiszy Ctrl + X, aby zakończyć działanie edytora.</span><span class="sxs-lookup"><span data-stu-id="43126-210">Once the change has been made, use Ctrl+X to exit the editor.</span></span> <span data-ttu-id="43126-211">Wybierz Y, a następnie wprowadź, aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="43126-211">Select Y, and then enter to save the changes.</span></span>

6. <span data-ttu-id="43126-212">Użyj `pig` polecenie, aby ponownie uruchomić powłoki.</span><span class="sxs-lookup"><span data-stu-id="43126-212">Use the `pig` command to start the shell again.</span></span> <span data-ttu-id="43126-213">Po przejściu na `grunt>` monit, użyj następującego do uruchamiania skryptu języka Python za pomocą interpreter języka Python C.</span><span class="sxs-lookup"><span data-stu-id="43126-213">Once you are at the `grunt>` prompt, use the following to run the Python script using the C Python interpreter.</span></span>

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="43126-214">Po zakończeniu tego zadania, co za wcześniej skryptu, za pomocą Jython powinna zostać wyświetlona tych samych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="43126-214">Once this job completes, you should see the same output as when you previously ran the script using Jython.</span></span>

### <a name="powershell-upload-the-files"></a><span data-ttu-id="43126-215">Środowiska PowerShell: Przekazywanie plików</span><span class="sxs-lookup"><span data-stu-id="43126-215">PowerShell: Upload the files</span></span>

<span data-ttu-id="43126-216">Można przekazać pliki do serwera HDInsight za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="43126-216">You can use PowerShell to upload the files to the HDInsight server.</span></span> <span data-ttu-id="43126-217">Aby przekazać pliki języka Python, użyj następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="43126-217">Use the following script to upload the Python files:</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="43126-218">Kroki opisane w tej sekcji, użyj programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="43126-218">The steps in this section use Azure PowerShell.</span></span> <span data-ttu-id="43126-219">Aby uzyskać więcej informacji na temat używania programu Azure PowerShell, zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="43126-219">For more information on using Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
# Change the path to match the file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload the file
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
> <span data-ttu-id="43126-220">Zmień `C:\path\to` wartość do ścieżki do plików na środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="43126-220">Change the `C:\path\to` value to the path to the files on your development environment.</span></span>

<span data-ttu-id="43126-221">Ten skrypt powoduje pobranie informacji o dla klastra usługi HDInsight, a następnie wyodrębnia konta i klucz dla domyślnego konta magazynu i operacji przekazywania plików do katalogu głównego kontenera.</span><span class="sxs-lookup"><span data-stu-id="43126-221">This script retrieves information for your HDInsight cluster, then extracts the account and key for the default storage account, and uploads the files to the root of the container.</span></span>

> [!NOTE]
> <span data-ttu-id="43126-222">Aby uzyskać więcej informacji dotyczących przekazywania plików, zobacz [przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight](hdinsight-upload-data.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="43126-222">For more information on uploading files, see the [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span></span>

#### <a name="powershell-use-the-hive-udf"></a><span data-ttu-id="43126-223">Środowiska PowerShell: Korzystanie z programu Hive funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="43126-223">PowerShell: Use the Hive UDF</span></span>

<span data-ttu-id="43126-224">Zdalne uruchamianie zapytań Hive można również programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="43126-224">PowerShell can also be used to remotely run Hive queries.</span></span> <span data-ttu-id="43126-225">Użyj następującego skryptu programu PowerShell do uruchamiania zapytań programu Hive, która używa **hiveudf.py** skryptu:</span><span class="sxs-lookup"><span data-stu-id="43126-225">Use the following PowerShell script to run a Hive query that uses **hiveudf.py** script:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43126-226">Przed uruchomieniem, skrypt monituje o informacje o koncie HTTPs/Admin dla klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="43126-226">Before running, the script prompts you for the HTTPs/Admin account information for your HDInsight cluster.</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

# If using a Windows-based HDInsight cluster, change the USING statement to:
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
Write-Host "Wait for the Hive job to complete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment the following to see stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="43126-227">Dane wyjściowe dla **Hive** zadanie powinno wyglądać podobnie do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="43126-227">The output for the **Hive** job should appear similar to the following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="43126-228">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="43126-228">Pig (Jython)</span></span>

<span data-ttu-id="43126-229">PowerShell mogą służyć do uruchamiania zadań Pig Latin.</span><span class="sxs-lookup"><span data-stu-id="43126-229">PowerShell can also be used to run Pig Latin jobs.</span></span> <span data-ttu-id="43126-230">Aby uruchomić zadanie Pig Latin, która używa **pigudf.py** skryptów, użyj następującego skryptu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="43126-230">To run a Pig Latin job that uses the **pigudf.py** script, use the following PowerShell script:</span></span>

> [!NOTE]
> <span data-ttu-id="43126-231">Gdy zdalne przesyłania zadania przy użyciu programu PowerShell, nie jest możliwe do użycia jako interpreter języka Python C.</span><span class="sxs-lookup"><span data-stu-id="43126-231">When remotely submitting a job using PowerShell, it is not possible to use C Python as the interpreter.</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

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

Write-Host "Wait for the Pig job to complete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment the following to see stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="43126-232">Dane wyjściowe dla **Pig** zadania powinna wyglądać podobnie do następujących danych:</span><span class="sxs-lookup"><span data-stu-id="43126-232">The output for the **Pig** job should appear similar to the following data:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <span data-ttu-id="43126-233"><a name="troubleshooting"></a>Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="43126-233"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="43126-234">Błędy podczas uruchamiania zadania</span><span class="sxs-lookup"><span data-stu-id="43126-234">Errors when running jobs</span></span>

<span data-ttu-id="43126-235">Podczas wykonywania zadania hive, może wystąpić błąd podobny do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="43126-235">When running the hive job, you may encounter an error similar to the following text:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing to your custom script. It may have crashed with an error.

<span data-ttu-id="43126-236">Ten problem może być spowodowane zakończenia wierszy w pliku języka Python.</span><span class="sxs-lookup"><span data-stu-id="43126-236">This problem may be caused by the line endings in the Python file.</span></span> <span data-ttu-id="43126-237">Wiele domyślne edytory systemu Windows przy użyciu CRLF jako zakończenie wiersza, ale aplikacje w systemie Linux zwykle oczekiwać wysuwu wiersza.</span><span class="sxs-lookup"><span data-stu-id="43126-237">Many Windows editors default to using CRLF as the line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="43126-238">Poniższe instrukcje środowiska PowerShell umożliwia Usuń znaki CR przed przekazaniem go do usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="43126-238">You can use the following PowerShell statements to remove the CR characters before uploading the file to HDInsight:</span></span>

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a><span data-ttu-id="43126-239">Skrypty programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="43126-239">PowerShell scripts</span></span>

<span data-ttu-id="43126-240">Zawierają zarówno przykładowe skrypty środowiska PowerShell służące do uruchamiania w przykładach komentarze wiersza, który wyświetla dane wyjściowe błędów dla zadania.</span><span class="sxs-lookup"><span data-stu-id="43126-240">Both of the example PowerShell scripts used to run the examples contain a commented line that displays error output for the job.</span></span> <span data-ttu-id="43126-241">Jeśli nie widzisz oczekiwane dane wyjściowe zadania, usuń znaczniki komentarza z następującego wiersza i zobacz, czy informacje o błędzie wskazuje na problem.</span><span class="sxs-lookup"><span data-stu-id="43126-241">If you are not seeing the expected output for the job, uncomment the following line and see if the error information indicates a problem.</span></span>

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="43126-242">Informacje o błędzie (STDERR) oraz wyniku zadania (STDOUT) również są rejestrowane w magazynie z usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="43126-242">The error information (STDERR) and the result of the job (STDOUT) are also logged to your HDInsight storage.</span></span>

| <span data-ttu-id="43126-243">Dla tego zadania...</span><span class="sxs-lookup"><span data-stu-id="43126-243">For this job...</span></span> | <span data-ttu-id="43126-244">Przyjrzyj się te pliki w kontenerze obiektów blob</span><span class="sxs-lookup"><span data-stu-id="43126-244">Look at these files in the blob container</span></span> |
| --- | --- |
| <span data-ttu-id="43126-245">Hive</span><span class="sxs-lookup"><span data-stu-id="43126-245">Hive</span></span> |<span data-ttu-id="43126-246">/ HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="43126-246">/HivePython/stderr</span></span><p><span data-ttu-id="43126-247">/ HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="43126-247">/HivePython/stdout</span></span> |
| <span data-ttu-id="43126-248">Pig</span><span class="sxs-lookup"><span data-stu-id="43126-248">Pig</span></span> |<span data-ttu-id="43126-249">/ PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="43126-249">/PigPython/stderr</span></span><p><span data-ttu-id="43126-250">/ PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="43126-250">/PigPython/stdout</span></span> |

## <span data-ttu-id="43126-251"><a name="next"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="43126-251"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="43126-252">Jeśli musisz załadować modułów środowiska Python, które domyślnie nie są dostępne, zobacz [wdrażanie modułu do usługi Azure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span><span class="sxs-lookup"><span data-stu-id="43126-252">If you need to load Python modules that aren't provided by default, see [How to deploy a module to Azure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="43126-253">Dla innych sposobów korzystania wieprzowy, Hive i aby dowiedzieć się więcej o korzystaniu z MapReduce, można znaleźć w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="43126-253">For other ways to use Pig, Hive, and to learn about using MapReduce, see the following documents:</span></span>

* [<span data-ttu-id="43126-254">Korzystanie z programu Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="43126-254">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="43126-255">Korzystanie z języka Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="43126-255">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="43126-256">Korzystać z usługi MapReduce z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="43126-256">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
