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
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="ff72b-103">Funkcje (UDF) za pomocą technologii Hive i Pig zdefiniowane przez użytkownika Python użycia w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ff72b-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="ff72b-104">Dowiedz się, jak toouse Python zdefiniowane przez użytkownika (UDF) funkcje za pomocą Apache Hive i Pig na platformie Hadoop w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ff72b-104">Learn how toouse Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="ff72b-105"><a name="python"></a>Python w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ff72b-105"><a name="python"></a>Python on HDInsight</span></span>

<span data-ttu-id="ff72b-106">Python2.7 jest instalowany domyślnie na HDInsight 3.0 i nowszych.</span><span class="sxs-lookup"><span data-stu-id="ff72b-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span></span> <span data-ttu-id="ff72b-107">Apache Hive można użyć z tą wersją języka Python dla przetwarzania strumienia.</span><span class="sxs-lookup"><span data-stu-id="ff72b-107">Apache Hive can be used with this version of Python for stream processing.</span></span> <span data-ttu-id="ff72b-108">Przetwarzanie strumienia używa STDOUT i STDIN danych toopass między Hive i hello funkcji zdefiniowanej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ff72b-108">Stream processing uses STDOUT and STDIN toopass data between Hive and hello UDF.</span></span>

<span data-ttu-id="ff72b-109">HDInsight obejmuje również Jython, który jest implementacją języka Python, napisany w języku Java.</span><span class="sxs-lookup"><span data-stu-id="ff72b-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="ff72b-110">Jython działa bezpośrednio na powitania maszyny wirtualnej Java i nie używa przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="ff72b-110">Jython runs directly on hello Java Virtual Machine and does not use streaming.</span></span> <span data-ttu-id="ff72b-111">Jython jest hello zalecane interpreter języka Python, korzystając z języka Pig języka Python.</span><span class="sxs-lookup"><span data-stu-id="ff72b-111">Jython is hello recommended Python interpreter when using Python with Pig.</span></span>

> [!WARNING]
> <span data-ttu-id="ff72b-112">kroki Hello w tym dokumencie upewnij hello następujące założenia:</span><span class="sxs-lookup"><span data-stu-id="ff72b-112">hello steps in this document make hello following assumptions:</span></span> 
>
> * <span data-ttu-id="ff72b-113">Witaj można utworzyć skrypty języka Python na środowiska deweloperskiego lokalnego.</span><span class="sxs-lookup"><span data-stu-id="ff72b-113">You create hello Python scripts on your local development environment.</span></span>
> * <span data-ttu-id="ff72b-114">Przekaż tooHDInsight skrypty hello przy użyciu albo hello `scp` polecenie sesji Bash lokalnej lub hello podany skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff72b-114">You upload hello scripts tooHDInsight using either hello `scp` command from a local Bash session or hello provided PowerShell script.</span></span>
>
> <span data-ttu-id="ff72b-115">Jeśli chcesz, aby toouse hello [powłoki chmury Azure (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) Podgląd toowork z usługą HDInsight, a następnie należy:</span><span class="sxs-lookup"><span data-stu-id="ff72b-115">If you want toouse hello [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview toowork with HDInsight, then you must:</span></span>
>
> * <span data-ttu-id="ff72b-116">Tworzenie skryptów hello w środowisku powłoki hello chmury.</span><span class="sxs-lookup"><span data-stu-id="ff72b-116">Create hello scripts inside hello cloud shell environment.</span></span>
> * <span data-ttu-id="ff72b-117">Użyj `scp` tooupload hello plików z hello chmury tooHDInsight powłoki.</span><span class="sxs-lookup"><span data-stu-id="ff72b-117">Use `scp` tooupload hello files from hello cloud shell tooHDInsight.</span></span>
> * <span data-ttu-id="ff72b-118">Użyj `ssh` z tooHDInsight tooconnect powłoki hello w chmurze i przykłady hello wykonywania.</span><span class="sxs-lookup"><span data-stu-id="ff72b-118">Use `ssh` from hello cloud shell tooconnect tooHDInsight and run hello examples.</span></span>

## <span data-ttu-id="ff72b-119"><a name="hivepython"></a>Hive funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="ff72b-119"><a name="hivepython"></a>Hive UDF</span></span>

<span data-ttu-id="ff72b-120">Python mogą być używane jako UDF z Hive za pośrednictwem hello HiveQL `TRANSFORM` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="ff72b-120">Python can be used as a UDF from Hive through hello HiveQL `TRANSFORM` statement.</span></span> <span data-ttu-id="ff72b-121">Na przykład po HiveQL hello wywołuje hello `hiveudf.py` plików przechowywanych w hello domyślne konto magazynu Azure hello klastra.</span><span class="sxs-lookup"><span data-stu-id="ff72b-121">For example, hello following HiveQL invokes hello `hiveudf.py` file stored in hello default Azure Storage account for hello cluster.</span></span>

<span data-ttu-id="ff72b-122">**HDInsight opartych na systemie Linux**</span><span class="sxs-lookup"><span data-stu-id="ff72b-122">**Linux-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="ff72b-123">**HDInsight opartych na systemie Windows**</span><span class="sxs-lookup"><span data-stu-id="ff72b-123">**Windows-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="ff72b-124">W klastrach HDInsight opartych na systemie Windows hello `USING` klauzula musi określać hello toopython.exe pełną ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="ff72b-124">On Windows-based HDInsight clusters, hello `USING` clause must specify hello full path toopython.exe.</span></span>

<span data-ttu-id="ff72b-125">Oto, co oznacza w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="ff72b-125">Here's what this example does:</span></span>

1. <span data-ttu-id="ff72b-126">Witaj `add file` instrukcji na początku hello pliku hello dodaje hello `hiveudf.py` toohello pliku rozproszonej pamięci podręcznej, więc nie jest dostępny przez wszystkie węzły w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="ff72b-126">hello `add file` statement at hello beginning of hello file adds hello `hiveudf.py` file toohello distributed cache, so it's accessible by all nodes in hello cluster.</span></span>
2. <span data-ttu-id="ff72b-127">Witaj `SELECT TRANSFORM ... USING` instrukcja wybiera danych z hello `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="ff72b-127">hello `SELECT TRANSFORM ... USING` statement selects data from hello `hivesampletable`.</span></span> <span data-ttu-id="ff72b-128">Przekazuje ono również hello clientid, devicemake i toohello wartości devicemodel `hiveudf.py` skryptu.</span><span class="sxs-lookup"><span data-stu-id="ff72b-128">It also passes hello clientid, devicemake, and devicemodel values toohello `hiveudf.py` script.</span></span>
3. <span data-ttu-id="ff72b-129">Witaj `AS` klauzuli opisuje pola hello zwrócony z `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="ff72b-129">hello `AS` clause describes hello fields returned from `hiveudf.py`.</span></span>

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a><span data-ttu-id="ff72b-130">Utwórz plik hiveudf.py hello</span><span class="sxs-lookup"><span data-stu-id="ff72b-130">Create hello hiveudf.py file</span></span>


<span data-ttu-id="ff72b-131">Na środowiska deweloperskiego, Utwórz plik tekstowy o nazwie `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="ff72b-131">On your development environment, create a text file named `hiveudf.py`.</span></span> <span data-ttu-id="ff72b-132">Użyj następującego kodu jako hello zawartość pliku hello hello:</span><span class="sxs-lookup"><span data-stu-id="ff72b-132">Use hello following code as hello contents of hello file:</span></span>

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

<span data-ttu-id="ff72b-133">Ten skrypt wykonuje hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="ff72b-133">This script performs hello following actions:</span></span>

1. <span data-ttu-id="ff72b-134">Odczytaj wiersz danych stdin.</span><span class="sxs-lookup"><span data-stu-id="ff72b-134">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="ff72b-135">Witaj, kończyć się znakiem nowego wiersza zostanie usunięty, za pomocą `string.strip(line, "\n ")`.</span><span class="sxs-lookup"><span data-stu-id="ff72b-135">hello trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="ff72b-136">Podczas przetwarzania strumienia, pojedynczy wiersz zawiera wszystkich wartości hello z znak tabulacji od każdej wartości.</span><span class="sxs-lookup"><span data-stu-id="ff72b-136">When doing stream processing, a single line contains all hello values with a tab character between each value.</span></span> <span data-ttu-id="ff72b-137">Dlatego `string.split(line, "\t")` mogą być używane toosplit hello danych wejściowych na każdej karcie zwracanie tylko pola hello.</span><span class="sxs-lookup"><span data-stu-id="ff72b-137">So `string.split(line, "\t")` can be used toosplit hello input at each tab, returning just hello fields.</span></span>
4. <span data-ttu-id="ff72b-138">Po zakończeniu przetwarzania danych wyjściowych hello musi być napisana tooSTDOUT jako pojedynczy wiersz z kartą między każdego pola.</span><span class="sxs-lookup"><span data-stu-id="ff72b-138">When processing is complete, hello output must be written tooSTDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="ff72b-139">Na przykład `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span><span class="sxs-lookup"><span data-stu-id="ff72b-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="ff72b-140">Witaj `while` pętli jest powtarzany do momentu nie `line` jest do odczytu.</span><span class="sxs-lookup"><span data-stu-id="ff72b-140">hello `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="ff72b-141">dane wyjściowe skryptu Hello jest złączeniem hello wartości wejściowe dla `devicemake` i `devicemodel`, oraz skrót hello połączonych wartości.</span><span class="sxs-lookup"><span data-stu-id="ff72b-141">hello script output is a concatenation of hello input values for `devicemake` and `devicemodel`, and a hash of hello concatenated value.</span></span>

<span data-ttu-id="ff72b-142">Zobacz [uruchamianie przykładów hello](#running) jak toorun w tym przykładzie w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ff72b-142">See [Running hello examples](#running) for how toorun this example on your HDInsight cluster.</span></span>

## <span data-ttu-id="ff72b-143"><a name="pigpython"></a>Pig funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="ff72b-143"><a name="pigpython"></a>Pig UDF</span></span>

<span data-ttu-id="ff72b-144">Skrypt w języku Python może służyć jako UDF z Pig za pośrednictwem hello `GENERATE` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="ff72b-144">A Python script can be used as a UDF from Pig through hello `GENERATE` statement.</span></span> <span data-ttu-id="ff72b-145">Można uruchomić skryptu hello za pomocą Jython lub C Python.</span><span class="sxs-lookup"><span data-stu-id="ff72b-145">You can run hello script using either Jython or C Python.</span></span>

* <span data-ttu-id="ff72b-146">Jython działa na powitania JVM i natywnie można wywołać z Pig.</span><span class="sxs-lookup"><span data-stu-id="ff72b-146">Jython runs on hello JVM, and can natively be called from Pig.</span></span>
* <span data-ttu-id="ff72b-147">C Python to proces zewnętrzny, więc dane hello z Pig na powitania JVM wysłaniu toohello skrypt uruchomiony w procesie Python.</span><span class="sxs-lookup"><span data-stu-id="ff72b-147">C Python is an external process, so hello data from Pig on hello JVM is sent out toohello script running in a Python process.</span></span> <span data-ttu-id="ff72b-148">dane wyjściowe Hello hello skrypt w języku Python są wysyłane do Pig.</span><span class="sxs-lookup"><span data-stu-id="ff72b-148">hello output of hello Python script is sent back into Pig.</span></span>

<span data-ttu-id="ff72b-149">interpreter języka Python hello toospecify, użyj `register` podczas odwoływania się do hello skrypt w języku Python.</span><span class="sxs-lookup"><span data-stu-id="ff72b-149">toospecify hello Python interpreter, use `register` when referencing hello Python script.</span></span> <span data-ttu-id="ff72b-150">Witaj następujące przykłady Zarejestruj skrypty Pig jako `myfuncs`:</span><span class="sxs-lookup"><span data-stu-id="ff72b-150">hello following examples register scripts with Pig as `myfuncs`:</span></span>

* <span data-ttu-id="ff72b-151">**toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="ff72b-151">**toouse Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="ff72b-152">**toouse C Python**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="ff72b-152">**toouse C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff72b-153">Podczas korzystania z Jython, hello ścieżki toohello pig_jython pliku może być ścieżką lokalną lub WASB: / / ścieżki.</span><span class="sxs-lookup"><span data-stu-id="ff72b-153">When using Jython, hello path toohello pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="ff72b-154">Jednak podczas korzystania z języka Python C, możesz odwoływać pliku w systemie pliku lokalnego hello węzła hello używasz zadania programu Pig hello toosubmit.</span><span class="sxs-lookup"><span data-stu-id="ff72b-154">However, when using C Python, you must reference a file on hello local file system of hello node that you are using toosubmit hello Pig job.</span></span>

<span data-ttu-id="ff72b-155">Po poza rejestracji hello Pig Latin w tym przykładzie hello sam zarówno dla:</span><span class="sxs-lookup"><span data-stu-id="ff72b-155">Once past registration, hello Pig Latin for this example is hello same for both:</span></span>

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="ff72b-156">Oto, co oznacza w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="ff72b-156">Here's what this example does:</span></span>

1. <span data-ttu-id="ff72b-157">pierwszy wiersz Hello ładuje hello przykładowy plik danych `sample.log` do `LOGS`.</span><span class="sxs-lookup"><span data-stu-id="ff72b-157">hello first line loads hello sample data file, `sample.log` into `LOGS`.</span></span> <span data-ttu-id="ff72b-158">Definiuje również każdego rekordu jako `chararray`.</span><span class="sxs-lookup"><span data-stu-id="ff72b-158">It also defines each record as a `chararray`.</span></span>
2. <span data-ttu-id="ff72b-159">następnego wiersza Hello odfiltrowuje wszystkie wartości null, hello wynik operacji hello do przechowywania `LOG`.</span><span class="sxs-lookup"><span data-stu-id="ff72b-159">hello next line filters out any null values, storing hello result of hello operation into `LOG`.</span></span>
3. <span data-ttu-id="ff72b-160">Następnie iteruje za pośrednictwem hello rekordów w `LOG` i używa `GENERATE` tooinvoke hello `create_structure` metody zawarte w skrypcie Python/Jython hello załadowany jako `myfuncs`.</span><span class="sxs-lookup"><span data-stu-id="ff72b-160">Next, it iterates over hello records in `LOG` and uses `GENERATE` tooinvoke hello `create_structure` method contained in hello Python/Jython script loaded as `myfuncs`.</span></span> <span data-ttu-id="ff72b-161">`LINE`jest używana toopass hello bieżącej funkcji toohello rekordów.</span><span class="sxs-lookup"><span data-stu-id="ff72b-161">`LINE` is used toopass hello current record toohello function.</span></span>
4. <span data-ttu-id="ff72b-162">Ponadto dane wyjściowe hello są zrzut tooSTDOUT przy użyciu hello `DUMP` polecenia.</span><span class="sxs-lookup"><span data-stu-id="ff72b-162">Finally, hello outputs are dumped tooSTDOUT using hello `DUMP` command.</span></span> <span data-ttu-id="ff72b-163">To polecenie wyświetla wyniki powitania po zakończeniu operacji hello.</span><span class="sxs-lookup"><span data-stu-id="ff72b-163">This command displays hello results after hello operation completes.</span></span>

### <a name="create-hello-pigudfpy-file"></a><span data-ttu-id="ff72b-164">Utwórz plik pigudf.py hello</span><span class="sxs-lookup"><span data-stu-id="ff72b-164">Create hello pigudf.py file</span></span>

<span data-ttu-id="ff72b-165">Na środowiska deweloperskiego, Utwórz plik tekstowy o nazwie `pigudf.py`.</span><span class="sxs-lookup"><span data-stu-id="ff72b-165">On your development environment, create a text file named `pigudf.py`.</span></span> <span data-ttu-id="ff72b-166">Użyj następującego kodu jako hello zawartość pliku hello hello:</span><span class="sxs-lookup"><span data-stu-id="ff72b-166">Use hello following code as hello contents of hello file:</span></span>

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

<span data-ttu-id="ff72b-167">Przykład Witaj Pig Latin zdefiniowanego hello `LINE` danych wejściowych jako chararray, ponieważ nie istnieje zgodny schematu dla danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="ff72b-167">In hello Pig Latin example, we defined hello `LINE` input as a chararray because there is no consistent schema for hello input.</span></span> <span data-ttu-id="ff72b-168">Witaj skrypt w języku Python przekształca hello danych w spójne schematu dla danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="ff72b-168">hello Python script transforms hello data into a consistent schema for output.</span></span>

1. <span data-ttu-id="ff72b-169">Witaj `@outputSchema` hello format danych zwracanych tooPig hello definiuje instrukcji.</span><span class="sxs-lookup"><span data-stu-id="ff72b-169">hello `@outputSchema` statement defines hello format of hello data that is returned tooPig.</span></span> <span data-ttu-id="ff72b-170">W takim przypadku ma **pakiet danych**, który jest typem danych Pig.</span><span class="sxs-lookup"><span data-stu-id="ff72b-170">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="ff72b-171">Witaj w zbiorze zawiera hello kolejnych pól, które są chararray (ciągi):</span><span class="sxs-lookup"><span data-stu-id="ff72b-171">hello bag contains hello following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="ff72b-172">Data — Witaj wpis dziennika hello Data utworzenia</span><span class="sxs-lookup"><span data-stu-id="ff72b-172">date - hello date hello log entry was created</span></span>
   * <span data-ttu-id="ff72b-173">raz — Witaj hello wpis dziennika został utworzony.</span><span class="sxs-lookup"><span data-stu-id="ff72b-173">time - hello time hello log entry was created</span></span>
   * <span data-ttu-id="ff72b-174">klasy — Witaj klasy nazwa hello zapis został utworzony dla</span><span class="sxs-lookup"><span data-stu-id="ff72b-174">classname - hello class name hello entry was created for</span></span>
   * <span data-ttu-id="ff72b-175">poziom — Witaj poziom dziennika</span><span class="sxs-lookup"><span data-stu-id="ff72b-175">level - hello log level</span></span>
   * <span data-ttu-id="ff72b-176">Szczegóły — pełne szczegóły hello wpis dziennika.</span><span class="sxs-lookup"><span data-stu-id="ff72b-176">detail - verbose details for hello log entry</span></span>

2. <span data-ttu-id="ff72b-177">Następnie hello `def create_structure(input)` definiuje funkcję hello, Pig przekazujący pozycji do.</span><span class="sxs-lookup"><span data-stu-id="ff72b-177">Next, hello `def create_structure(input)` defines hello function that Pig passes line items to.</span></span>

3. <span data-ttu-id="ff72b-178">Witaj przykładowe dane `sample.log`, przede wszystkim zgodne toohello dzień, godzina classname poziomu i szczegółów chcemy tooreturn schematu.</span><span class="sxs-lookup"><span data-stu-id="ff72b-178">hello example data, `sample.log`, mostly conforms toohello date, time, classname, level, and detail schema we want tooreturn.</span></span> <span data-ttu-id="ff72b-179">Jednak zawiera kilka wierszy, które zaczynają się od `*java.lang.Exception*`.</span><span class="sxs-lookup"><span data-stu-id="ff72b-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span></span> <span data-ttu-id="ff72b-180">Te wiersze musi być zmodyfikowany toomatch hello schematu.</span><span class="sxs-lookup"><span data-stu-id="ff72b-180">These lines must be modified toomatch hello schema.</span></span> <span data-ttu-id="ff72b-181">Witaj `if` instrukcji wyszukuje, a następnie masażystów hello hello toomove danych wejściowych `*java.lang.Exception*` celu toohello ciąg dostarczają hello danych w linii z naszych schematu oczekiwane dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="ff72b-181">hello `if` statement checks for those, then massages hello input data toomove hello `*java.lang.Exception*` string toohello end, bringing hello data in-line with our expected output schema.</span></span>

4. <span data-ttu-id="ff72b-182">Następnie hello `split` polecenia jest używane toosplit hello danych na powitania pierwsze cztery miejsca znaków.</span><span class="sxs-lookup"><span data-stu-id="ff72b-182">Next, hello `split` command is used toosplit hello data at hello first four space characters.</span></span> <span data-ttu-id="ff72b-183">dane wyjściowe Hello jest przypisany do `date`, `time`, `classname`, `level`, i `detail`.</span><span class="sxs-lookup"><span data-stu-id="ff72b-183">hello output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span></span>

5. <span data-ttu-id="ff72b-184">Na koniec hello wartości są zwracane tooPig.</span><span class="sxs-lookup"><span data-stu-id="ff72b-184">Finally, hello values are returned tooPig.</span></span>

<span data-ttu-id="ff72b-185">Po zwróceniu danych hello tooPig, ma schemat spójny, zgodnie z definicją w hello `@outputSchema` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="ff72b-185">When hello data is returned tooPig, it has a consistent schema as defined in hello `@outputSchema` statement.</span></span>

## <span data-ttu-id="ff72b-186"><a name="running"></a>Przekaż, a następnie uruchom hello przykłady</span><span class="sxs-lookup"><span data-stu-id="ff72b-186"><a name="running"></a>Upload and run hello examples</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff72b-187">Witaj **SSH** kroki pracować tylko z klastra usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="ff72b-187">hello **SSH** steps only work with a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="ff72b-188">Witaj **PowerShell** kroki pracy z klastra z systemem Linux lub HDInsight opartych na systemie Windows, ale wymaga klienta systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="ff72b-188">hello **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span></span>

### <a name="ssh"></a><span data-ttu-id="ff72b-189">SSH</span><span class="sxs-lookup"><span data-stu-id="ff72b-189">SSH</span></span>

<span data-ttu-id="ff72b-190">Aby uzyskać więcej informacji o korzystaniu z protokołu SSH, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ff72b-190">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="ff72b-191">Użyj `scp` klastra usługi HDInsight tooyour toocopy hello plików.</span><span class="sxs-lookup"><span data-stu-id="ff72b-191">Use `scp` toocopy hello files tooyour HDInsight cluster.</span></span> <span data-ttu-id="ff72b-192">Na przykład Witaj następujące polecenia kopie hello pliki tooa klastra o nazwie **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="ff72b-192">For example, hello following command copies hello files tooa cluster named **mycluster**.</span></span>

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. <span data-ttu-id="ff72b-193">Używanie protokołu SSH tooconnect toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="ff72b-193">Use SSH tooconnect toohello cluster.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="ff72b-194">W sesji SSH hello dodanie plików python hello wcześniej przekazany toohello WASB magazyn dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="ff72b-194">From hello SSH session, add hello python files uploaded previously toohello WASB storage for hello cluster.</span></span>

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

<span data-ttu-id="ff72b-195">Po przekazaniu plików hello, użyj następujących hello kroki toorun hello Hive i Pig zadania.</span><span class="sxs-lookup"><span data-stu-id="ff72b-195">After uploading hello files, use hello following steps toorun hello Hive and Pig jobs.</span></span>

#### <a name="use-hello-hive-udf"></a><span data-ttu-id="ff72b-196">Użyj hello Hive funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="ff72b-196">Use hello Hive UDF</span></span>

1. <span data-ttu-id="ff72b-197">Użyj hello `hive` toostart hello hive powłoki poleceń.</span><span class="sxs-lookup"><span data-stu-id="ff72b-197">Use hello `hive` command toostart hello hive shell.</span></span> <span data-ttu-id="ff72b-198">Powinny pojawić się `hive>` Monituj po załadowaniu hello powłoki.</span><span class="sxs-lookup"><span data-stu-id="ff72b-198">You should see a `hive>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="ff72b-199">Wprowadź hello następującego zapytania na powitania `hive>` wiersza:</span><span class="sxs-lookup"><span data-stu-id="ff72b-199">Enter hello following query at hello `hive>` prompt:</span></span>

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. <span data-ttu-id="ff72b-200">Po wprowadzeniu hello ostatni wiersz, należy zacząć hello zadania.</span><span class="sxs-lookup"><span data-stu-id="ff72b-200">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="ff72b-201">Po zakończeniu zadania hello zwraca dane wyjściowe toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="ff72b-201">Once hello job completes, it returns output similar toohello following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a><span data-ttu-id="ff72b-202">Użyj hello Pig UDF</span><span class="sxs-lookup"><span data-stu-id="ff72b-202">Use hello Pig UDF</span></span>

1. <span data-ttu-id="ff72b-203">Użyj hello `pig` toostart hello powłoki poleceń.</span><span class="sxs-lookup"><span data-stu-id="ff72b-203">Use hello `pig` command toostart hello shell.</span></span> <span data-ttu-id="ff72b-204">Zostanie wyświetlony `grunt>` Monituj po załadowaniu hello powłoki.</span><span class="sxs-lookup"><span data-stu-id="ff72b-204">You see a `grunt>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="ff72b-205">Wprowadź następujące instrukcje na powitania hello `grunt>` wiersza:</span><span class="sxs-lookup"><span data-stu-id="ff72b-205">Enter hello following statements at hello `grunt>` prompt:</span></span>

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="ff72b-206">Po wprowadzeniu hello następującego wiersza, należy zacząć hello zadania.</span><span class="sxs-lookup"><span data-stu-id="ff72b-206">After entering hello following line, hello job should start.</span></span> <span data-ttu-id="ff72b-207">Po zakończeniu zadania hello zwraca dane wyjściowe toohello podobne następujące dane:</span><span class="sxs-lookup"><span data-stu-id="ff72b-207">Once hello job completes, it returns output similar toohello following data:</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="ff72b-208">Użyj `quit` tooexit hello Grunt powłoki, a następnie użyj hello poniższe tooedit hello pigudf.py plik na powitania lokalnego systemu plików:</span><span class="sxs-lookup"><span data-stu-id="ff72b-208">Use `quit` tooexit hello Grunt shell, and then use hello following tooedit hello pigudf.py file on hello local file system:</span></span>

    ```bash
    nano pigudf.py
    ```

5. <span data-ttu-id="ff72b-209">Raz w edytorze hello, usuń znaczniki komentarza powitania po wierszu przez usunięcie hello `#` znaku od początku hello hello wiersza:</span><span class="sxs-lookup"><span data-stu-id="ff72b-209">Once in hello editor, uncomment hello following line by removing hello `#` character from hello beginning of hello line:</span></span>

    ```bash
    #from pig_util import outputSchema
    ```

    <span data-ttu-id="ff72b-210">Po hello zmiany zostały wprowadzone, należy użyć edytora hello tooexit Ctrl + X.</span><span class="sxs-lookup"><span data-stu-id="ff72b-210">Once hello change has been made, use Ctrl+X tooexit hello editor.</span></span> <span data-ttu-id="ff72b-211">Wybierz Y, a następnie wprowadź zmiany hello toosave.</span><span class="sxs-lookup"><span data-stu-id="ff72b-211">Select Y, and then enter toosave hello changes.</span></span>

6. <span data-ttu-id="ff72b-212">Użyj hello `pig` polecenia powłoki hello toostart ponownie.</span><span class="sxs-lookup"><span data-stu-id="ff72b-212">Use hello `pig` command toostart hello shell again.</span></span> <span data-ttu-id="ff72b-213">Po przejściu na powitania `grunt>` monit, użyj następującego skryptu Python hello toorun za pomocą interpreter języka Python C hello hello.</span><span class="sxs-lookup"><span data-stu-id="ff72b-213">Once you are at hello `grunt>` prompt, use hello following toorun hello Python script using hello C Python interpreter.</span></span>

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="ff72b-214">Po zakończeniu tego zadania, co za wcześniej hello skryptu za pomocą Jython powinna zostać wyświetlona hello sam wyjściowy.</span><span class="sxs-lookup"><span data-stu-id="ff72b-214">Once this job completes, you should see hello same output as when you previously ran hello script using Jython.</span></span>

### <a name="powershell-upload-hello-files"></a><span data-ttu-id="ff72b-215">Środowiska PowerShell: Pliki hello przekazywania</span><span class="sxs-lookup"><span data-stu-id="ff72b-215">PowerShell: Upload hello files</span></span>

<span data-ttu-id="ff72b-216">Można użyć programu PowerShell tooupload hello plików toohello HDInsight serwera.</span><span class="sxs-lookup"><span data-stu-id="ff72b-216">You can use PowerShell tooupload hello files toohello HDInsight server.</span></span> <span data-ttu-id="ff72b-217">Użyj hello następujące pliki Python hello tooupload skryptu:</span><span class="sxs-lookup"><span data-stu-id="ff72b-217">Use hello following script tooupload hello Python files:</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ff72b-218">kroki Hello w tej sekcji, użyj programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff72b-218">hello steps in this section use Azure PowerShell.</span></span> <span data-ttu-id="ff72b-219">Aby uzyskać więcej informacji na temat używania programu Azure PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ff72b-219">For more information on using Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

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
> <span data-ttu-id="ff72b-220">Zmień hello `C:\path\to` wartość toohello ścieżka toohello plików na środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="ff72b-220">Change hello `C:\path\to` value toohello path toohello files on your development environment.</span></span>

<span data-ttu-id="ff72b-221">Ten skrypt powoduje pobranie informacji o dla klastra usługi HDInsight, a następnie wyodrębnia hello konta i klucz dla hello domyślne konto magazynu i przekazywanie hello głównego toohello pliki hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="ff72b-221">This script retrieves information for your HDInsight cluster, then extracts hello account and key for hello default storage account, and uploads hello files toohello root of hello container.</span></span>

> [!NOTE]
> <span data-ttu-id="ff72b-222">Aby uzyskać więcej informacji dotyczących przekazywania plików, zobacz hello [przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight](hdinsight-upload-data.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="ff72b-222">For more information on uploading files, see hello [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span></span>

#### <a name="powershell-use-hello-hive-udf"></a><span data-ttu-id="ff72b-223">Programu PowerShell: Hello Hive UDF Użyj</span><span class="sxs-lookup"><span data-stu-id="ff72b-223">PowerShell: Use hello Hive UDF</span></span>

<span data-ttu-id="ff72b-224">PowerShell może być również używane tooremotely uruchamiania zapytań Hive.</span><span class="sxs-lookup"><span data-stu-id="ff72b-224">PowerShell can also be used tooremotely run Hive queries.</span></span> <span data-ttu-id="ff72b-225">Użyj powitania po toorun skrypt programu PowerShell zapytań programu Hive, która używa **hiveudf.py** skryptu:</span><span class="sxs-lookup"><span data-stu-id="ff72b-225">Use hello following PowerShell script toorun a Hive query that uses **hiveudf.py** script:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff72b-226">Przed uruchomieniem, skrypt hello monituje o hello HTTPs/Admin informacje o koncie dla klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ff72b-226">Before running, hello script prompts you for hello HTTPs/Admin account information for your HDInsight cluster.</span></span>

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

<span data-ttu-id="ff72b-227">Witaj danych wyjściowych dla hello **Hive** zadania powinien zostać wyświetlony toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="ff72b-227">hello output for hello **Hive** job should appear similar toohello following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="ff72b-228">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="ff72b-228">Pig (Jython)</span></span>

<span data-ttu-id="ff72b-229">PowerShell może być również używane toorun Pig Latin zadania.</span><span class="sxs-lookup"><span data-stu-id="ff72b-229">PowerShell can also be used toorun Pig Latin jobs.</span></span> <span data-ttu-id="ff72b-230">toorun zadania Pig Latin, który używa hello **pigudf.py** skryptu, użyj następującego skryptu programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="ff72b-230">toorun a Pig Latin job that uses hello **pigudf.py** script, use hello following PowerShell script:</span></span>

> [!NOTE]
> <span data-ttu-id="ff72b-231">Gdy zdalne przesyłania zadania przy użyciu programu PowerShell, nie jest możliwe toouse C Python jako hello interpreter.</span><span class="sxs-lookup"><span data-stu-id="ff72b-231">When remotely submitting a job using PowerShell, it is not possible toouse C Python as hello interpreter.</span></span>

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

<span data-ttu-id="ff72b-232">Witaj danych wyjściowych dla hello **Pig** zadania powinien zostać wyświetlony podobne toohello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="ff72b-232">hello output for hello **Pig** job should appear similar toohello following data:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <span data-ttu-id="ff72b-233"><a name="troubleshooting"></a>Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="ff72b-233"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="ff72b-234">Błędy podczas uruchamiania zadania</span><span class="sxs-lookup"><span data-stu-id="ff72b-234">Errors when running jobs</span></span>

<span data-ttu-id="ff72b-235">Podczas uruchamiania zadania hive hello, może wystąpić błąd podobny toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="ff72b-235">When running hello hive job, you may encounter an error similar toohello following text:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

<span data-ttu-id="ff72b-236">Ten problem może być spowodowane hello zakończenia wierszy w pliku języka Python hello.</span><span class="sxs-lookup"><span data-stu-id="ff72b-236">This problem may be caused by hello line endings in hello Python file.</span></span> <span data-ttu-id="ff72b-237">Wiele edytorów Windows domyślne toousing CRLF jako wiersz hello zakończenia, ale zwykle LF aplikacje w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="ff72b-237">Many Windows editors default toousing CRLF as hello line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="ff72b-238">Program hello następujące znaki hello CR tooremove instrukcje PowerShell przed przekazaniem tooHDInsight pliku hello:</span><span class="sxs-lookup"><span data-stu-id="ff72b-238">You can use hello following PowerShell statements tooremove hello CR characters before uploading hello file tooHDInsight:</span></span>

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a><span data-ttu-id="ff72b-239">Skrypty programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff72b-239">PowerShell scripts</span></span>

<span data-ttu-id="ff72b-240">Przykładu hello skryptów programu PowerShell używanych toorun hello przykłady zawierają komentarze wiersza, który wyświetla dane wyjściowe błędów hello zadania.</span><span class="sxs-lookup"><span data-stu-id="ff72b-240">Both of hello example PowerShell scripts used toorun hello examples contain a commented line that displays error output for hello job.</span></span> <span data-ttu-id="ff72b-241">Jeśli nie widzisz hello oczekuje danych wyjściowych zadania hello, usuń znaczniki komentarza hello następujący wiersz i zobacz, czy informacje o błędzie hello wskazuje na problem.</span><span class="sxs-lookup"><span data-stu-id="ff72b-241">If you are not seeing hello expected output for hello job, uncomment hello following line and see if hello error information indicates a problem.</span></span>

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="ff72b-242">informacje o błędzie Hello (STDERR) oraz hello wyniku zadania hello (STDOUT) są również zarejestrowane tooyour magazynu usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ff72b-242">hello error information (STDERR) and hello result of hello job (STDOUT) are also logged tooyour HDInsight storage.</span></span>

| <span data-ttu-id="ff72b-243">Dla tego zadania...</span><span class="sxs-lookup"><span data-stu-id="ff72b-243">For this job...</span></span> | <span data-ttu-id="ff72b-244">Przyjrzyj się te pliki w kontenerze obiektów blob hello</span><span class="sxs-lookup"><span data-stu-id="ff72b-244">Look at these files in hello blob container</span></span> |
| --- | --- |
| <span data-ttu-id="ff72b-245">Hive</span><span class="sxs-lookup"><span data-stu-id="ff72b-245">Hive</span></span> |<span data-ttu-id="ff72b-246">/ HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="ff72b-246">/HivePython/stderr</span></span><p><span data-ttu-id="ff72b-247">/ HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="ff72b-247">/HivePython/stdout</span></span> |
| <span data-ttu-id="ff72b-248">Pig</span><span class="sxs-lookup"><span data-stu-id="ff72b-248">Pig</span></span> |<span data-ttu-id="ff72b-249">/ PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="ff72b-249">/PigPython/stderr</span></span><p><span data-ttu-id="ff72b-250">/ PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="ff72b-250">/PigPython/stdout</span></span> |

## <span data-ttu-id="ff72b-251"><a name="next"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ff72b-251"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="ff72b-252">Jeśli potrzebujesz tooload modułów środowiska Python, które domyślnie nie są dostępne, zobacz [jak toodeploy tooAzure modułu HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff72b-252">If you need tooload Python modules that aren't provided by default, see [How toodeploy a module tooAzure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="ff72b-253">Inne sposoby toouse Pig, Hive i toolearn o korzystaniu z MapReduce Zobacz hello w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="ff72b-253">For other ways toouse Pig, Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="ff72b-254">Korzystanie z programu Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="ff72b-254">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ff72b-255">Korzystanie z języka Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="ff72b-255">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ff72b-256">Korzystać z usługi MapReduce z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="ff72b-256">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
