---
title: "Podręcznik programowania U-SQL dla usługi Azure Data Lake | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zbiór usług w usłudze Azure Data Lake, które umożliwiają tworzenie platformy danych big data oparte na chmurze."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
ms.assetid: 63be271e-7c44-4d19-9897-c2913ee9599d
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: saveenr
ms.openlocfilehash: e4e298475d7be7d51c8bd55be498371ed6ce77a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="99449-103">Podręcznik programowania U-SQL</span><span class="sxs-lookup"><span data-stu-id="99449-103">U-SQL programmability guide</span></span>

<span data-ttu-id="99449-104">U-SQL jest język zapytania, które jest przeznaczone do typów danych dużych obciążeń.</span><span class="sxs-lookup"><span data-stu-id="99449-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="99449-105">Jedną z funkcji unikatowy U-SQL jest kombinacją języka deklaratywne przypominającego SQL z rozszerzeń i programowania, który znajduje się w języku C#.</span><span class="sxs-lookup"><span data-stu-id="99449-105">One of the unique features of U-SQL is the combination of the SQL-like declarative language with the extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="99449-106">W tym przewodniku możemy skupić się na rozszerzania i programowania języka U-SQL, który został włączony w języku C#.</span><span class="sxs-lookup"><span data-stu-id="99449-106">In this guide, we concentrate on the extensibility and programmability of the U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="99449-107">Wymagania</span><span class="sxs-lookup"><span data-stu-id="99449-107">Requirements</span></span>

<span data-ttu-id="99449-108">Pobierz i zainstaluj [Azure Data Lake Tools dla programu Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="99449-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="99449-109">Wprowadzenie do języka U-SQL</span><span class="sxs-lookup"><span data-stu-id="99449-109">Get started with U-SQL</span></span>  

<span data-ttu-id="99449-110">Przyjrzyjmy się poniższy skrypt U-SQL:</span><span class="sxs-lookup"><span data-stu-id="99449-110">Let’s look at the following U-SQL script:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso",   1500.0, "2017-03-39"),
            ("Woodgrove", 2700.0, "2017-04-10")
        ) AS 
              D( customer, amount );
@results =
    SELECT
        customer,
    amount,
    date
    FROM @a;    
```

<span data-ttu-id="99449-111">Definiuje zestawu wierszy o nazwie @a i tworzy zestawu wierszy o nazwie @results z @a.</span><span class="sxs-lookup"><span data-stu-id="99449-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="99449-112">Typy C# i wyrażenia w skryptu U-SQL</span><span class="sxs-lookup"><span data-stu-id="99449-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="99449-113">Wyrażenie U-SQL jest wyrażenie C# połączone z operacji logicznych U-SQL takich `AND`, `OR`, i `NOT`.</span><span class="sxs-lookup"><span data-stu-id="99449-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="99449-114">Wyrażenia języka U-SQL mogą być używane z SELECT, EXTRACT, gdzie wystąpienia, Grupuj według, ZADEKLAROWAĆ.</span><span class="sxs-lookup"><span data-stu-id="99449-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="99449-115">Na przykład poniższy skrypt analizuje ciągu na wartość daty i godziny w klauzuli SELECT.</span><span class="sxs-lookup"><span data-stu-id="99449-115">For example, the following script parses a string a DateTime value in the SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="99449-116">Poniższy skrypt analizuje ciągu na wartość daty i godziny w instrukcji DECLARE.</span><span class="sxs-lookup"><span data-stu-id="99449-116">The following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="99449-117">Używanie wyrażeń C# dla konwersje typów danych</span><span class="sxs-lookup"><span data-stu-id="99449-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="99449-118">W poniższym przykładzie pokazano, jak data/godzina konwersji danych za pomocą wyrażeń C#.</span><span class="sxs-lookup"><span data-stu-id="99449-118">The following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="99449-119">W tym scenariuszu określonego ciągu danych daty i godziny jest konwertowana na format daty i godziny o północy 00:00:00 czasu notacji.</span><span class="sxs-lookup"><span data-stu-id="99449-119">In this particular scenario, string datetime data is converted to standard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="99449-120">Używanie wyrażeń C# dla bieżącej daty</span><span class="sxs-lookup"><span data-stu-id="99449-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="99449-121">Możliwość ściągania dzisiaj, możemy użyć następującego wyrażenia języka C#:</span><span class="sxs-lookup"><span data-stu-id="99449-121">To pull today’s date, we can use the following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="99449-122">Poniżej przedstawiono przykład sposobu użycia tego wyrażenia w skrypcie:</span><span class="sxs-lookup"><span data-stu-id="99449-122">Here's an example of how to use this expression in a script:</span></span>

```
@rs1 =
    SELECT
        MAX(guid) AS start_id,
        MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        user,
        des
    FROM @rs0
    GROUP BY user, des;
```



## <a name="using-net-assemblies"></a><span data-ttu-id="99449-123">Za pomocą zestawów platformy .NET</span><span class="sxs-lookup"><span data-stu-id="99449-123">Using .NET assemblies</span></span>
<span data-ttu-id="99449-124">U-SQL modelu rozszerzalności odgrywa możliwość dodawania niestandardowych kodów.</span><span class="sxs-lookup"><span data-stu-id="99449-124">U-SQL’s extensibility model relies heavily on the ability to add custom code.</span></span> <span data-ttu-id="99449-125">Obecnie U-SQL zapewnia łatwy sposób, aby dodać własne firmy Microsoft. Kod na podstawie sieci (w szczególności, C#).</span><span class="sxs-lookup"><span data-stu-id="99449-125">Currently, U-SQL provides you with easy ways to add your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="99449-126">Jednak można również dodać kodu niestandardowego, który jest zapisywany w innych językach .NET, takie jak VB.NET lub F #.</span><span class="sxs-lookup"><span data-stu-id="99449-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="99449-127">Rejestrowanie zestawów platformy .NET</span><span class="sxs-lookup"><span data-stu-id="99449-127">Register a .NET assembly</span></span>

<span data-ttu-id="99449-128">Użyj instrukcji instrukcja CREATE ASSEMBLY można umieścić zestaw .NET do języka U-SQL bazy danych.</span><span class="sxs-lookup"><span data-stu-id="99449-128">Use the CREATE ASSEMBLY statement to place a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="99449-129">Po zestaw znajduje się w bazie danych, skryptów U-SQL można użyć tych zestawów przy użyciu instrukcji odwołanie do zestawu.</span><span class="sxs-lookup"><span data-stu-id="99449-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using the REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="99449-130">Poniższy kod przedstawia sposób rejestrowania zestawu:</span><span class="sxs-lookup"><span data-stu-id="99449-130">The following code shows how to register an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="99449-131">Poniższy kod przedstawia sposób odwołanie do zestawu:</span><span class="sxs-lookup"><span data-stu-id="99449-131">The following code shows how to reference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="99449-132">Zapoznaj się [instrukcje rejestracji zestawu](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) który obejmuje w tym temacie bardziej szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="99449-132">Consult the [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="99449-133">Użyj wersji zestawu</span><span class="sxs-lookup"><span data-stu-id="99449-133">Use assembly versioning</span></span>
<span data-ttu-id="99449-134">Obecnie U-SQL używa .NET Framework w wersji 4.5.</span><span class="sxs-lookup"><span data-stu-id="99449-134">Currently, U-SQL uses the .NET Framework version 4.5.</span></span> <span data-ttu-id="99449-135">Dlatego upewnij się, że własne zestawy są zgodne z tą wersją środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="99449-135">So ensure that your own assemblies are compatible with that version of the runtime.</span></span>

<span data-ttu-id="99449-136">Jak wspomniano wcześniej, kod działa U-SQL w formacie 64-bitowej (x 64).</span><span class="sxs-lookup"><span data-stu-id="99449-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="99449-137">Tak upewnij się, że kod jest skompilowana do uruchamiania na x64.</span><span class="sxs-lookup"><span data-stu-id="99449-137">So make sure that your code is compiled to run on x64.</span></span> <span data-ttu-id="99449-138">W przeciwnym razie błąd niepoprawny format przedstawiona wcześniej.</span><span class="sxs-lookup"><span data-stu-id="99449-138">Otherwise you get the incorrect format error shown earlier.</span></span>

<span data-ttu-id="99449-139">Każdy przekazany zestaw biblioteki DLL i pliku zasobów, takich jak innego środowiska uruchomieniowego, natywny zestaw lub pliku konfiguracji, może mieć maksymalnie 400 MB.</span><span class="sxs-lookup"><span data-stu-id="99449-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="99449-140">Całkowity rozmiar wdrożonych zasobów za pomocą wdrażania zasobów lub za pomocą odwołania do zestawów i ich dodatkowe pliki, nie może przekraczać 3 GB.</span><span class="sxs-lookup"><span data-stu-id="99449-140">The total size of deployed resources, either via DEPLOY RESOURCE or via references to assemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="99449-141">Na koniec należy pamiętać, że każda baza danych U-SQL może zawierać tylko jedną wersję żadnych danego zestawu.</span><span class="sxs-lookup"><span data-stu-id="99449-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="99449-142">Na przykład jeśli potrzebujesz zarówno w wersji 7, jak i w wersji 8 biblioteki NewtonSoft Json.Net, musisz zarejestrować je w dwóch różnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="99449-142">For example, if you need both version 7 and version 8 of the NewtonSoft Json.Net library, you need to register them in two different databases.</span></span> <span data-ttu-id="99449-143">Ponadto każdy skrypt może odwoływać się tylko do jednej wersji danego zestawu biblioteki DLL.</span><span class="sxs-lookup"><span data-stu-id="99449-143">Furthermore, each script can only refer to one version of a given assembly DLL.</span></span> <span data-ttu-id="99449-144">W związku z tym U-SQL następuje C# zestawu zarządzania i wersji semantykę.</span><span class="sxs-lookup"><span data-stu-id="99449-144">In this respect, U-SQL follows the C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="99449-145">Użyj funkcji zdefiniowanej przez użytkownika: funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="99449-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="99449-146">Funkcje zdefiniowane przez użytkownika U-SQL lub funkcji zdefiniowanej przez użytkownika, są programowania procedur, które akceptują parametrów, wykonywania akcji (na przykład złożonych obliczeń) i zwraca wynik tego działania jako wartość.</span><span class="sxs-lookup"><span data-stu-id="99449-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return the result of that action as a value.</span></span> <span data-ttu-id="99449-147">Wartość zwracana funkcji zdefiniowanej przez użytkownika może być tylko jeden skalarnej.</span><span class="sxs-lookup"><span data-stu-id="99449-147">The return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="99449-148">UDF języka U-SQL może zostać wywołany w podstawowej skryptu U-SQL, takich jak wszystkie inne C# skalarną.</span><span class="sxs-lookup"><span data-stu-id="99449-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="99449-149">Firma Microsoft zaleca, aby zainicjować U-SQL funkcje zdefiniowane przez użytkownika jako **publicznego** i **statycznych**.</span><span class="sxs-lookup"><span data-stu-id="99449-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="99449-150">Pierwszy Przyjrzyjmy się prosty przykład tworzenia funkcji zdefiniowanej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-150">First let’s look at the simple example of creating a UDF.</span></span>

<span data-ttu-id="99449-151">W tym scenariuszu przypadek użycia należy ustalić okres, w tym kwartał i miesiąc obrachunkowy przy pierwszym logowaniu dla określonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-151">In this use-case scenario, we need to determine the fiscal period, including the fiscal quarter and fiscal month of the first sign-in for the specific user.</span></span> <span data-ttu-id="99449-152">Pierwszy miesiąc obrachunkowy roku w naszym scenariuszu jest czerwca.</span><span class="sxs-lookup"><span data-stu-id="99449-152">The first fiscal month of the year in our scenario is June.</span></span>

<span data-ttu-id="99449-153">Aby obliczyć okres, wprowadzeniu następujących funkcji języka C#:</span><span class="sxs-lookup"><span data-stu-id="99449-153">To calculate fiscal period, we introduce the following C# function:</span></span>

```
public static string GetFiscalPeriod(DateTime dt)
{
    int FiscalMonth=0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter=0;
    if (FiscalMonth >=1 && FiscalMonth<=3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return "Q" + FiscalQuarter.ToString() + ":P" + FiscalMonth.ToString();
}
```

<span data-ttu-id="99449-154">Po prostu oblicza miesiąc obrachunkowy i kwartał i zwraca wartość typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="99449-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="99449-155">Czerwca pierwszy miesiąc pierwszy kwartał obrachunkowy, możemy użyć "Q1:P1".</span><span class="sxs-lookup"><span data-stu-id="99449-155">For June, the first month of the first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="99449-156">Lipca możemy użyć "Q1:P2" i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="99449-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="99449-157">Jest to zwykły C# funkcję, która firma Microsoft ma być używane w naszych projektu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="99449-157">This is a regular C# function that we are going to use in our U-SQL project.</span></span>

<span data-ttu-id="99449-158">Oto, jak wygląda sekcji kodu powiązanego w tym scenariuszu:</span><span class="sxs-lookup"><span data-stu-id="99449-158">Here is how the code-behind section looks in this scenario:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        public static string GetFiscalPeriod(DateTime dt)
        {
            int FiscalMonth=0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter=0;
            if (FiscalMonth >=1 && FiscalMonth<=3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return "Q" + FiscalQuarter.ToString() + ":" + FiscalMonth.ToString();
        }

    }

}
```

<span data-ttu-id="99449-159">Teraz zamierzamy wywołanie tej funkcji z podstawowej skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="99449-159">Now we are going to call this function from the base U-SQL script.</span></span> <span data-ttu-id="99449-160">Aby to zrobić, musimy udostępnić w pełni kwalifikowaną nazwę funkcji, łącznie z przestrzenią nazw, która jest w tym przypadku NameSpace.Class.Function(parameter).</span><span class="sxs-lookup"><span data-stu-id="99449-160">To do this, we have to provide a fully qualified name for the function, including the namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="99449-161">Rzeczywiste podstawowy skrypt U-SQL jest następujący:</span><span class="sxs-lookup"><span data-stu-id="99449-161">Following is the actual U-SQL base script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt DateTime,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

DECLARE @default_dt DateTime = Convert.ToDateTime("06/01/2016");

@rs1 =
    SELECT
        MAX(guid) AS start_id,
    MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        user,
        des
    FROM @rs0
    GROUP BY user, des;

OUTPUT @rs1 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="99449-162">Poniżej znajduje się plik wyjściowy wykonywania skryptów:</span><span class="sxs-lookup"><span data-stu-id="99449-162">Following is the output file of the script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="99449-163">W tym przykładzie przedstawiono prosty użycie wbudowanej funkcji zdefiniowanej przez użytkownika w języku U-SQL.</span><span class="sxs-lookup"><span data-stu-id="99449-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="99449-164">Zachowaj stanu między wywołań funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="99449-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="99449-165">Obiekty programowania U-SQL C# można można bardziej zaawansowane opcje, wykorzystując interakcyjności za pomocą zmiennych globalnych związane z kodem.</span><span class="sxs-lookup"><span data-stu-id="99449-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through the code-behind global variables.</span></span> <span data-ttu-id="99449-166">Przyjrzyjmy się następujące scenariusza biznesowego w przypadku użycia.</span><span class="sxs-lookup"><span data-stu-id="99449-166">Let’s look at the following business use-case scenario.</span></span>

<span data-ttu-id="99449-167">W dużych organizacjach użytkownicy mogą przełączać odmian wewnętrznych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="99449-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="99449-168">Obejmują one programu Microsoft Dynamics CRM, usługa Power Bi i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="99449-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="99449-169">Klienci mogą mają dotyczyć analizy danych telemetrycznych sposób użytkownicy będą przełączać się między różnymi aplikacjami, jakie są trendy użycia, i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="99449-169">Customers might want to apply a telemetry analysis of how users switch between different applications, what the usage trends are, and so on.</span></span> <span data-ttu-id="99449-170">Jest celem w firmie w celu zoptymalizowania użycia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="99449-170">The goal for the business is to optimize application usage.</span></span> <span data-ttu-id="99449-171">Może być połączyć różnych aplikacji lub określonych procedur logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="99449-171">They also might want to combine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="99449-172">Na osiągnięcie tego celu, musimy określić identyfikatory sesji i zwłoki czas od ostatniej sesji, który wystąpił.</span><span class="sxs-lookup"><span data-stu-id="99449-172">To achieve this goal, we have to determine session IDs and lag time between the last session that occurred.</span></span>

<span data-ttu-id="99449-173">Musimy Znajdź poprzednie logowanie, a następnie przypisz to logowanie do wszystkich sesji, które są generowane na tej samej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="99449-173">We need to find a previous sign-in and then assign this sign-in to all sessions that are being generated to the same application.</span></span> <span data-ttu-id="99449-174">Pierwszego wyzwania jest, że podstawowy skrypt U-SQL nie umożliwiają nałożenia obliczeń na już obliczane kolumny z funkcja LAG.</span><span class="sxs-lookup"><span data-stu-id="99449-174">The first challenge is that U-SQL base script doesn't allow us to apply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="99449-175">Drugie żądanie jest mamy zachować określonej sesji dla wszystkich sesji, w tym samym okresie czasu.</span><span class="sxs-lookup"><span data-stu-id="99449-175">The second challenge is that we have to keep the specific session for all sessions within the same time period.</span></span>

<span data-ttu-id="99449-176">Aby rozwiązać ten problem, używamy wewnątrz sekcji kodem — zmienna globalna: `static public string globalSession;`.</span><span class="sxs-lookup"><span data-stu-id="99449-176">To solve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="99449-177">Tę zmienną globalną jest stosowana do całego zestawu wierszy podczas wykonywania naszych skryptu.</span><span class="sxs-lookup"><span data-stu-id="99449-177">This global variable is applied to the entire rowset during our script execution.</span></span>

<span data-ttu-id="99449-178">Oto sekcji CodeBehind nasz program U-SQL:</span><span class="sxs-lookup"><span data-stu-id="99449-178">Here is the code-behind section of our U-SQL program:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQLApplication21
{
    public class UserSession
    {
        static public string globalSession;
        static public string StampUserSession(string eventTime, string PreviousRow, string Session)
        {

            if (!string.IsNullOrEmpty(PreviousRow))
            {
                double timeGap = Convert.ToDateTime(eventTime).Subtract(Convert.ToDateTime(PreviousRow)).TotalMinutes;
                if (timeGap <= 60) {return Session;}
                else {return Guid.NewGuid().ToString();}
            }
            else {return Guid.NewGuid().ToString();}

        }

        static public string getStampUserSession(string Session)
        {
            if (Session != globalSession && !string.IsNullOrEmpty(Session)) { globalSession = Session; }
            return globalSession;
        }

    }
}
```

<span data-ttu-id="99449-179">W tym przykładzie pokazano zmiennej globalnej `static public string globalSession;` używany wewnątrz `getStampUserSession` funkcji i uzyskiwanie za każdym parametrze sesji zostanie zmieniona.</span><span class="sxs-lookup"><span data-stu-id="99449-179">This example shows the global variable `static public string globalSession;` used inside the `getStampUserSession` function and getting reinitialized each time the Session parameter is changed.</span></span>

<span data-ttu-id="99449-180">Podstawowy skrypt U-SQL jest następujący:</span><span class="sxs-lookup"><span data-stu-id="99449-180">The U-SQL base script is as follows:</span></span>

```
DECLARE @in string = @"\UserSession\test1.tsv";
DECLARE @out1 string = @"\UserSession\Out1.csv";
DECLARE @out2 string = @"\UserSession\Out2.csv";
DECLARE @out3 string = @"\UserSession\Out3.csv";

@records =
    EXTRACT DataId string,
            EventDateTime string,           
            UserName string,
            UserSessionTimestamp string

    FROM @in
    USING Extractors.Tsv();

@rs1 =
    SELECT 
        EventDateTime,
        UserName,
    LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,          
        string.IsNullOrEmpty(LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,           
        USQLApplication21.UserSession.StampUserSession
           (
            EventDateTime,
            LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC),
            LAG(UserSessionTimestamp, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)
           ) AS UserSessionTimestamp
    FROM @records;

@rs2 =
    SELECT 
        EventDateTime,
        UserName,
        LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,
        string.IsNullOrEmpty( LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,
        USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp) AS UserSessionTimestamp
    FROM @rs1
    WHERE UserName != "UserName";

OUTPUT @rs2
    TO @out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

<span data-ttu-id="99449-181">Funkcja `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` jest tutaj wywoływana podczas obliczania drugiego zestawu wierszy pamięci.</span><span class="sxs-lookup"><span data-stu-id="99449-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during the second memory rowset calculation.</span></span> <span data-ttu-id="99449-182">Przekazuje ono `UserSessionTimestamp` kolumny i zwraca wartość do `UserSessionTimestamp` została zmieniona.</span><span class="sxs-lookup"><span data-stu-id="99449-182">It passes the `UserSessionTimestamp` column and returns the value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="99449-183">Plik wyjściowy jest następujący:</span><span class="sxs-lookup"><span data-stu-id="99449-183">The output file is as follows:</span></span>

```
"2016-02-19T07:32:36.8420000-08:00","User1",,True,"72a0660e-22df-428e-b672-e0977007177f"
"2016-02-17T11:52:43.6350000-08:00","User2",,True,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-17T11:59:08.8320000-08:00","User2","2016-02-17T11:52:43.6350000-08:00",False,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-11T07:04:17.2630000-08:00","User3",,True,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-11T07:10:33.9720000-08:00","User3","2016-02-11T07:04:17.2630000-08:00",False,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-15T21:27:41.8210000-08:00","User3","2016-02-11T07:10:33.9720000-08:00",False,"4d2bc48d-bdf3-4591-a9c1-7b15ceb8e074"
"2016-02-16T05:48:49.6360000-08:00","User3","2016-02-15T21:27:41.8210000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-16T06:22:43.6390000-08:00","User3","2016-02-16T05:48:49.6360000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-17T16:29:53.2280000-08:00","User3","2016-02-16T06:22:43.6390000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T16:39:07.2430000-08:00","User3","2016-02-17T16:29:53.2280000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T17:20:39.3220000-08:00","User3","2016-02-17T16:39:07.2430000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-19T05:23:54.5710000-08:00","User3","2016-02-17T17:20:39.3220000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T05:48:37.7510000-08:00","User3","2016-02-19T05:23:54.5710000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T06:40:27.4830000-08:00","User3","2016-02-19T05:48:37.7510000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T07:27:37.7550000-08:00","User3","2016-02-19T06:40:27.4830000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T19:35:40.9450000-08:00","User3","2016-02-19T07:27:37.7550000-08:00",False,"3f385f0b-3e68-4456-ac74-ff6cef093674"
"2016-02-20T00:07:37.8250000-08:00","User3","2016-02-19T19:35:40.9450000-08:00",False,"685f76d5-ca48-4c58-b77d-bd3a9ddb33da"
"2016-02-11T09:01:33.9720000-08:00","User4",,True,"9f0cf696-c8ba-449a-8d5f-1ca6ed8f2ee8"
"2016-02-17T06:30:38.6210000-08:00","User4","2016-02-11T09:01:33.9720000-08:00",False,"8b11fd2a-01bf-4a5e-a9af-3c92c4e4382a"
"2016-02-17T22:15:26.4020000-08:00","User4","2016-02-17T06:30:38.6210000-08:00",False,"4e1cb707-3b5f-49c1-90c7-9b33b86ca1f4"
"2016-02-18T14:37:27.6560000-08:00","User4","2016-02-17T22:15:26.4020000-08:00",False,"f4e44400-e837-40ed-8dfd-2ea264d4e338"
"2016-02-19T01:20:31.4800000-08:00","User4","2016-02-18T14:37:27.6560000-08:00",False,"2136f4cf-7c7d-43c1-8ae2-08f4ad6a6e08"
```

<span data-ttu-id="99449-184">W tym przykładzie przedstawiono bardziej skomplikowane scenariusz przypadek użycia, w którym firma Microsoft przy użyciu zmiennej globalnej wewnątrz sekcji związane z kodem, który jest stosowany do wierszy całej pamięci.</span><span class="sxs-lookup"><span data-stu-id="99449-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied to the entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="99449-185">Używanie typów zdefiniowanych przez użytkownika: UDT</span><span class="sxs-lookup"><span data-stu-id="99449-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="99449-186">Typy definiowane przez użytkownika lub UDT, jest inna funkcja programowalności U-SQL.</span><span class="sxs-lookup"><span data-stu-id="99449-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="99449-187">UDT U-SQL zachowuje się jak zwykły C# zdefiniowane przez użytkownika typu.</span><span class="sxs-lookup"><span data-stu-id="99449-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="99449-188">C# to silnie typizowaną język, który zezwala na korzystanie z wbudowane i niestandardowe typy danych zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-188">C# is a strongly typed language that allows the use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="99449-189">U-SQL nie można niejawnie serializacji lub zdeserializować dowolnego UDTs podczas przekazywania UDT między wierzchołków w zestawów wierszy.</span><span class="sxs-lookup"><span data-stu-id="99449-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when the UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="99449-190">Oznacza to, że użytkownik musi podać jawne elementu formatującego za pomocą interfejsu IFormatter.</span><span class="sxs-lookup"><span data-stu-id="99449-190">This means that the user has to provide an explicit formatter by using the IFormatter interface.</span></span> <span data-ttu-id="99449-191">To zapewnia serializacja U-SQL i zdeserializować metody dla typu.</span><span class="sxs-lookup"><span data-stu-id="99449-191">This provides U-SQL with the serialize and de-serialize methods for the UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="99449-192">U-SQL ekstraktory wbudowanych i outputters obecnie nie można serializować lub zdeserializować UDT danych do i z plików, nawet w przypadku zestawu IFormatter.</span><span class="sxs-lookup"><span data-stu-id="99449-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data to or from files even with the IFormatter set.</span></span> <span data-ttu-id="99449-193">Dlatego podczas zapisywania danych UDT pliku z instrukcją dane wyjściowe, lub odczytywania go z katalogu, należy przekazać ją w postaci ciągu lub tablicy typu byte.</span><span class="sxs-lookup"><span data-stu-id="99449-193">So when you're writing UDT data to a file with the OUTPUT statement, or reading it with an extractor, you have to pass it as a string or byte array.</span></span> <span data-ttu-id="99449-194">Następnie wywołaj serializacji i deserializacji jawnie kodu (to znaczy metodę ToString() UDT).</span><span class="sxs-lookup"><span data-stu-id="99449-194">Then you call the serialization and deserialization code (that is, the UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="99449-195">Zdefiniowane przez użytkownika ekstraktory i outputters, z drugiej strony, można odczytują i zapisują typów.</span><span class="sxs-lookup"><span data-stu-id="99449-195">User-defined extractors and outputters, on the other hand, can read and write UDTs.</span></span>

<span data-ttu-id="99449-196">Jeśli firma Microsoft spróbuj użyć UDT w katalogu lub OUTPUTTER (Brak poprzedniej wybierz), jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="99449-196">If we try to use UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="99449-197">Firma Microsoft komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="99449-197">We receive the following error:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used to output column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how to serialize this type, or call a serialization method on the type in
the preceding SELECT.   C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

<span data-ttu-id="99449-198">Aby pracować z UDT w outputter, albo mamy do serializacji ciągu z metodę ToString() lub tworzenie niestandardowych outputter.</span><span class="sxs-lookup"><span data-stu-id="99449-198">To work with UDT in outputter, we either have to serialize it to string with the ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="99449-199">Typów nie można obecnie używać w GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="99449-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="99449-200">Jeśli UDT jest używany w GROUP BY, zostanie zgłoszony następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="99449-200">If UDT is used in GROUP BY, the following error is thrown:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want to use with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

<span data-ttu-id="99449-201">Aby zdefiniować UDT, musimy:</span><span class="sxs-lookup"><span data-stu-id="99449-201">To define a UDT, we have to:</span></span>

* <span data-ttu-id="99449-202">Dodaj następujących przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="99449-202">Add the following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="99449-203">Dodaj `Microsoft.Analytics.Interfaces`, co jest wymagane dla interfejsów UDT.</span><span class="sxs-lookup"><span data-stu-id="99449-203">Add `Microsoft.Analytics.Interfaces`, which is required for the UDT interfaces.</span></span> <span data-ttu-id="99449-204">Ponadto `System.IO` mogą być wymagane do zdefiniowania interfejsu IFormatter.</span><span class="sxs-lookup"><span data-stu-id="99449-204">In addition, `System.IO` might be needed to define the IFormatter interface.</span></span>

* <span data-ttu-id="99449-205">Zdefiniuj typ zdefiniowane z atrybutem SqlUserDefinedType.</span><span class="sxs-lookup"><span data-stu-id="99449-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="99449-206">**SqlUserDefinedType** służy do oznaczania definicja typu w zestawie jako typ zdefiniowany przez użytkownika (UDT) w języku U-SQL.</span><span class="sxs-lookup"><span data-stu-id="99449-206">**SqlUserDefinedType** is used to mark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="99449-207">Właściwości w ustawieniach atrybutu odzwierciedlają charakterystyki fizycznej UDT.</span><span class="sxs-lookup"><span data-stu-id="99449-207">The properties on the attribute reflect the physical characteristics of the UDT.</span></span> <span data-ttu-id="99449-208">Ta klasa nie może być dziedziczona.</span><span class="sxs-lookup"><span data-stu-id="99449-208">This class cannot be inherited.</span></span>

<span data-ttu-id="99449-209">SqlUserDefinedType jest wymagany atrybut UDT definicji.</span><span class="sxs-lookup"><span data-stu-id="99449-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="99449-210">Konstruktor klasy:</span><span class="sxs-lookup"><span data-stu-id="99449-210">The constructor of the class:</span></span>  

* <span data-ttu-id="99449-211">SqlUserDefinedTypeAttribute (elementu formatującego typu)</span><span class="sxs-lookup"><span data-stu-id="99449-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="99449-212">Program formatujący typ: wymaganego parametru do definiowania elementu formatującego UDT — w szczególności typ `IFormatter` interfejsu muszą być przekazywane w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="99449-212">Type formatter: Required parameter to define an UDT formatter--specifically, the type of the `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="99449-213">Typowy UDT wymaga również definicji interfejsu IFormatter, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="99449-213">Typical UDT also requires definition of the IFormatter interface, as shown in the following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="99449-214">`IFormatter` Interfejsu serializuje i zwalnia serializuje wykres obiektu z typem głównego \<typeparamref name = "T" >.</span><span class="sxs-lookup"><span data-stu-id="99449-214">The `IFormatter` interface serializes and de-serializes an object graph with the root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="99449-215">\<typeparam name = "T" > typu głównego do serializacji i deserializacji wykresu obiektu.</span><span class="sxs-lookup"><span data-stu-id="99449-215">\<typeparam name="T">The root type for the object graph to serialize and de-serialize.</span></span>

* <span data-ttu-id="99449-216">**Deserializacja**: cofnąć serializuje dane dla podanego strumienia i reconstitutes wykresu obiektów.</span><span class="sxs-lookup"><span data-stu-id="99449-216">**Deserialize**: De-serializes the data on the provided stream and reconstitutes the graph of objects.</span></span>

* <span data-ttu-id="99449-217">**Serializować**: Serializuje obiekt lub grafu obiektów z danym elementem głównym do dostarczonego strumienia.</span><span class="sxs-lookup"><span data-stu-id="99449-217">**Serialize**: Serializes an object, or graph of objects, with the given root to the provided stream.</span></span>

<span data-ttu-id="99449-218">`MyType`wystąpienie: wystąpienie typu.</span><span class="sxs-lookup"><span data-stu-id="99449-218">`MyType` instance: Instance of the type.</span></span>  
<span data-ttu-id="99449-219">`IColumnWriter`Moduł zapisujący / `IColumnReader` czytnika: zasadniczy strumień kolumny.</span><span class="sxs-lookup"><span data-stu-id="99449-219">`IColumnWriter` writer / `IColumnReader` reader: The underlying column stream.</span></span>  
<span data-ttu-id="99449-220">`ISerializationContext`kontekst: wyliczenia, który definiuje zestaw flagi Określa kontekst źródła lub miejsca docelowego dla tego strumienia podczas serializacji.</span><span class="sxs-lookup"><span data-stu-id="99449-220">`ISerializationContext` context: Enum that defines a set of flags that specifies the source or destination context for the stream during serialization.</span></span>

* <span data-ttu-id="99449-221">**Pośredni**: Określa, czy kontekst źródłowy lub docelowy nie jest utrwalonego magazynu.</span><span class="sxs-lookup"><span data-stu-id="99449-221">**Intermediate**: Specifies that the source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="99449-222">**Trwałość**: Określa, że źródłowy lub docelowy kontekst magazynu trwałego.</span><span class="sxs-lookup"><span data-stu-id="99449-222">**Persistence**: Specifies that the source or destination context is a persisted store.</span></span>

<span data-ttu-id="99449-223">Jako regularne C# typ, definicji UDT U-SQL mogą zawierać zastąpień dla operatorów takich jak +/ == /! =.</span><span class="sxs-lookup"><span data-stu-id="99449-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="99449-224">Może również obejmować metod statycznych.</span><span class="sxs-lookup"><span data-stu-id="99449-224">It can also include static methods.</span></span> <span data-ttu-id="99449-225">Na przykład, jeśli firma Microsoft będzie używany ten UDT jako parametr do funkcji agregujących MIN U-SQL, musimy zdefiniować < zastąpienie operatora.</span><span class="sxs-lookup"><span data-stu-id="99449-225">For example, if we are going to use this UDT as a parameter to a U-SQL MIN aggregate function, we have to define < operator override.</span></span>

<span data-ttu-id="99449-226">Wcześniej w tym przewodniku firma Microsoft przedstawiono przykład obrachunkowym identyfikacji okresu od określonej daty w formacie Qn:Pn (Q1:P10).</span><span class="sxs-lookup"><span data-stu-id="99449-226">Earlier in this guide, we demonstrated an example for fiscal period identification from the specific date in the format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="99449-227">Poniższy przykład przedstawia sposób definiowania typu niestandardowego dla wartości okresu obrachunkowym.</span><span class="sxs-lookup"><span data-stu-id="99449-227">The following example shows how to define a custom type for fiscal period values.</span></span>

<span data-ttu-id="99449-228">Poniżej przedstawiono przykład sekcji kodu powiązanego z niestandardowy interfejs UDT i IFormatter:</span><span class="sxs-lookup"><span data-stu-id="99449-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

```
[SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
public struct FiscalPeriod
{
    public int Quarter { get; private set; }

    public int Month { get; private set; }

    public FiscalPeriod(int quarter, int month):this()
    {
    this.Quarter = quarter;
    this.Month = month;
    }

    public override bool Equals(object obj)
    {
    if (ReferenceEquals(null, obj))
    {
        return false;
    }

    return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
    }

    public bool Equals(FiscalPeriod other)
    {
return this.Quarter.Equals(other.Quarter) && this.Month.Equals(other.Month);
    }

    public bool GreaterThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
    }

    public bool LessThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
    }

    public override int GetHashCode()
    {
    unchecked
    {
        return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
    }
    }

    public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
    {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
    }

    public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.Equals(c2);
    }

    public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
    {
    return !c1.Equals(c2);
    }
    public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.GreaterThan(c2);
    }
    public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.LessThan(c2);
    }
    public override string ToString()
    {
    return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
    }

}

public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
{
    public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
    {
    using (var binaryWriter = new BinaryWriter(writer.BaseStream))
    {
        binaryWriter.Write(instance.Quarter);
        binaryWriter.Write(instance.Month);
        binaryWriter.Flush();
    }
    }

    public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
    {
    using (var binaryReader = new BinaryReader(reader.BaseStream))
    {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
        return result;
    }
    }
}
```

<span data-ttu-id="99449-229">Zdefiniowanego typu zawiera dwie liczb: kwartał i miesiąc.</span><span class="sxs-lookup"><span data-stu-id="99449-229">The defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="99449-230">Operatory == /! = / > / < a statyczną metodę ToString() są zdefiniowane w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="99449-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="99449-231">Jak wspomniano wcześniej, można używać w wyrażeniach wybierz UDT, ale nie można używać w OUTPUTTER/EKSTRAKTOR bez niestandardowej serializacji.</span><span class="sxs-lookup"><span data-stu-id="99449-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="99449-232">Go ma być serializowana w postaci ciągu z ToString() albo używane z niestandardowych OUTPUTTER/WYODRĘBNIANIA.</span><span class="sxs-lookup"><span data-stu-id="99449-232">It either has to be serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="99449-233">Teraz omówimy użycia UDT.</span><span class="sxs-lookup"><span data-stu-id="99449-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="99449-234">W sekcji związane z kodem możemy zmienione naszych funkcja GetFiscalPeriod do następującego:</span><span class="sxs-lookup"><span data-stu-id="99449-234">In a code-behind section, we changed our GetFiscalPeriod function to the following:</span></span>

```
public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
{
    int FiscalMonth = 0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter = 0;
    if (FiscalMonth >= 1 && FiscalMonth <= 3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return new FiscalPeriod(FiscalQuarter, FiscalMonth);
}
```

<span data-ttu-id="99449-235">Jak widać, zwraca wartość typu naszych FiscalPeriod.</span><span class="sxs-lookup"><span data-stu-id="99449-235">As you can see, it returns the value of our FiscalPeriod type.</span></span>

<span data-ttu-id="99449-236">W tym miejscu udostępniamy przykładem użyć go dalej w podstawowej skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="99449-236">Here we provide an example of how to use it further in U-SQL base script.</span></span> <span data-ttu-id="99449-237">W tym przykładzie przedstawiono różne formy UDT wywołanie skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="99449-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

```
DECLARE @input_file string = @"c:\work\cosmos\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"c:\work\cosmos\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid string,
        dt DateTime,
        user String,
        des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT 
        guid AS start_id,
        dt,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Quarter AS fiscalquarter,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Month AS fiscalmonth,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt) + new USQL_Programmability.CustomFunctions.FiscalPeriod(1,7) AS fiscalperiod_adjusted,
        user,
        des
    FROM @rs0;

@rs2 =
    SELECT 
           start_id,
           dt,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           fiscalquarter,
           fiscalmonth,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS fiscalperiod,

       // This user-defined type was created in the prior SELECT.  Passing the UDT to this subsequent SELECT would have failed if the UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="99449-238">Oto przykład pełnego kodem sekcji:</span><span class="sxs-lookup"><span data-stu-id="99449-238">Here's an example of a full code-behind section:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        static public DateTime? ToDateTime(string dt)
        {
            DateTime dtValue;

            if (!DateTime.TryParse(dt, out dtValue))
                return Convert.ToDateTime(dt);
            else
                return null;
        }

        public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
        {
            int FiscalMonth = 0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter = 0;
            if (FiscalMonth >= 1 && FiscalMonth <= 3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return new FiscalPeriod(FiscalQuarter, FiscalMonth);
        }



        [SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
        public struct FiscalPeriod
        {
            public int Quarter { get; private set; }

            public int Month { get; private set; }

            public FiscalPeriod(int quarter, int month):this()
            {
                this.Quarter = quarter;
                this.Month = month;
            }

            public override bool Equals(object obj)
            {
                if (ReferenceEquals(null, obj))
                {
                    return false;
                }

                return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
            }

            public bool Equals(FiscalPeriod other)
            {
return this.Quarter.Equals(other.Quarter) &&    this.Month.Equals(other.Month);
            }

            public bool GreaterThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
            }

            public bool LessThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
            }

            public override int GetHashCode()
            {
                unchecked
                {
                    return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
                }
            }

            public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
            {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
            }

            public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.Equals(c2);
            }

            public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
            {
                return !c1.Equals(c2);
            }
            public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.GreaterThan(c2);
            }
            public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.LessThan(c2);
            }
            public override string ToString()
            {
                return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
            }

        }

        public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
        {
public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
            {
                using (var binaryWriter = new BinaryWriter(writer.BaseStream))
                {
                    binaryWriter.Write(instance.Quarter);
                    binaryWriter.Write(instance.Month);
                    binaryWriter.Flush();
                }
            }

public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
            {
                using (var binaryReader = new BinaryReader(reader.BaseStream))
                {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
                    return result;
                }
            }
        }
    }
}
```

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="99449-239">Użyj agregacje zdefiniowane przez użytkownika: UDAGG</span><span class="sxs-lookup"><span data-stu-id="99449-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="99449-240">Agregacje zdefiniowane przez użytkownika są wszystkie funkcje związane z agregacji, które są niewysłanych out-of--box języku U-SQL.</span><span class="sxs-lookup"><span data-stu-id="99449-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="99449-241">Przykład może być agregacją, aby wykonać obliczenia matematyczne niestandardowych, konkatenacji ciągów, manipulacje z ciągów itd.</span><span class="sxs-lookup"><span data-stu-id="99449-241">The example can be an aggregate to perform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="99449-242">Zdefiniowane przez użytkownika agregacji klasy podstawowej definicji jest następujący:</span><span class="sxs-lookup"><span data-stu-id="99449-242">The user-defined aggregate base class definition is as follows:</span></span>

```c#
    [SqlUserDefinedAggregate]
    public abstract class IAggregate<T1, T2, TResult> : IAggregate
    {
        protected IAggregate();

        public abstract void Accumulate(T1 t1, T2 t2);
        public abstract void Init();
        public abstract TResult Terminate();
    }
```

<span data-ttu-id="99449-243">**SqlUserDefinedAggregate** wskazuje, że typ powinien zostać zarejestrowany jako agregacji zdefiniowanej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-243">**SqlUserDefinedAggregate** indicates that the type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="99449-244">Ta klasa nie może być dziedziczona.</span><span class="sxs-lookup"><span data-stu-id="99449-244">This class cannot be inherited.</span></span>

<span data-ttu-id="99449-245">Atrybut SqlUserDefinedType jest **opcjonalne** UDAGG definicji.</span><span class="sxs-lookup"><span data-stu-id="99449-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="99449-246">Klasa podstawowa umożliwia przekazywanie trzy parametry abstrakcyjne: dwa jako parametry wejściowe i jeden w wyniku.</span><span class="sxs-lookup"><span data-stu-id="99449-246">The base class allows you to pass three abstract parameters: two as input parameters and one as the result.</span></span> <span data-ttu-id="99449-247">Typy danych są zmienne i powinien być zdefiniowany podczas dziedziczenia klas.</span><span class="sxs-lookup"><span data-stu-id="99449-247">The data types are variable and should be defined during class inheritance.</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    { … }

    public override void Accumulate(string guid, string user)
    { … }

    public override string Terminate()
    { … }
}
```

* <span data-ttu-id="99449-248">**Init** wywołuje jeden raz dla każdej grupy podczas obliczania.</span><span class="sxs-lookup"><span data-stu-id="99449-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="99449-249">Procedura inicjowania zapewnia dla każdej grupy agregacji.</span><span class="sxs-lookup"><span data-stu-id="99449-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="99449-250">**Accumulate** jest wykonywane raz dla każdej wartości.</span><span class="sxs-lookup"><span data-stu-id="99449-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="99449-251">Udostępnia ona funkcje głównego dla algorytmu agregacji.</span><span class="sxs-lookup"><span data-stu-id="99449-251">It provides the main functionality for the aggregation algorithm.</span></span> <span data-ttu-id="99449-252">Może służyć do wartości zagregowanych z różnych typów danych, które są zdefiniowane podczas dziedziczenia klas.</span><span class="sxs-lookup"><span data-stu-id="99449-252">It can be used to aggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="99449-253">Może akceptować dwa parametry o typach danych zmiennej.</span><span class="sxs-lookup"><span data-stu-id="99449-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="99449-254">**Przerwanie** jest wykonywane raz dla każdej grupy agregacji po zakończeniu przetwarzania zwracać wynik dla każdej grupy.</span><span class="sxs-lookup"><span data-stu-id="99449-254">**Terminate** is executed once per aggregation group at the end of processing to output the result for each group.</span></span>

<span data-ttu-id="99449-255">Aby zadeklarować poprawne dane wejściowe i typów danych wyjściowych, użyj definicji klasy w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="99449-255">To declare correct input and output data types, use the class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="99449-256">T1: Pierwszy parametr accumulate</span><span class="sxs-lookup"><span data-stu-id="99449-256">T1: First parameter to accumulate</span></span>
* <span data-ttu-id="99449-257">T2: Pierwszy parametr accumulate</span><span class="sxs-lookup"><span data-stu-id="99449-257">T2: First parameter to accumulate</span></span>
* <span data-ttu-id="99449-258">TResult: Zwracany typ przerwania</span><span class="sxs-lookup"><span data-stu-id="99449-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="99449-259">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="99449-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="99449-260">lub</span><span class="sxs-lookup"><span data-stu-id="99449-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="99449-261">Użyj UDAGG w języku U-SQL</span><span class="sxs-lookup"><span data-stu-id="99449-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="99449-262">Aby użyć UDAGG, zdefiniuj je w CodeBehind lub odwołania z istniejących programowania DLL zgodnie z wcześniejszym opisem.</span><span class="sxs-lookup"><span data-stu-id="99449-262">To use UDAGG, first define it in code-behind or reference it from the existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="99449-263">Następnie należy użyć następującej składni:</span><span class="sxs-lookup"><span data-stu-id="99449-263">Then use the following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="99449-264">Oto przykład UDAGG:</span><span class="sxs-lookup"><span data-stu-id="99449-264">Here is an example of UDAGG:</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    {
        guid_agg = "";
    }

    public override void Accumulate(string guid, string user)
    {
        if (user.ToUpper()== "USER1")
        {
        guid_agg += "{" + guid + "}";
        }
    }

    public override string Terminate()
    {
        return guid_agg;
    }

}
```

<span data-ttu-id="99449-265">I podstawowego skryptu U-SQL:</span><span class="sxs-lookup"><span data-stu-id="99449-265">And base U-SQL script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @" \usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    SELECT
        user,
        AGG<USQL_Programmability.GuidAggregate>(guid,user) AS guid_list
    FROM @rs0
    GROUP BY user;

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="99449-266">W tym scenariuszu przypadek użycia możemy łączenie identyfikatorów GUID klas dla określonych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="99449-266">In this use-case scenario, we concatenate class GUIDs for the specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="99449-267">Za pomocą obiektów zdefiniowanych przez użytkownika: UDO</span><span class="sxs-lookup"><span data-stu-id="99449-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="99449-268">U-SQL umożliwia zdefiniowanie programowania niestandardowych obiektów, które są nazywane obiekty zdefiniowane przez użytkownika lub UDO.</span><span class="sxs-lookup"><span data-stu-id="99449-268">U-SQL enables you to define custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="99449-269">Poniżej przedstawiono listę UDO w języku U-SQL:</span><span class="sxs-lookup"><span data-stu-id="99449-269">The following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="99449-270">Ekstraktory zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="99449-270">User-defined extractors</span></span>
    * <span data-ttu-id="99449-271">Wyodrębnij wiersz po wierszu</span><span class="sxs-lookup"><span data-stu-id="99449-271">Extract row by row</span></span>
    * <span data-ttu-id="99449-272">Używane do implementowania wyodrębniania danych z niestandardowej strukturze plików</span><span class="sxs-lookup"><span data-stu-id="99449-272">Used to implement data extraction from custom structured files</span></span>

* <span data-ttu-id="99449-273">Outputters zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="99449-273">User-defined outputters</span></span>
    * <span data-ttu-id="99449-274">Dane wyjściowe wiersz po wierszu</span><span class="sxs-lookup"><span data-stu-id="99449-274">Output row by row</span></span>
    * <span data-ttu-id="99449-275">Używane do danych wyjściowych niestandardowe typy danych lub niestandardowego pliku formatów</span><span class="sxs-lookup"><span data-stu-id="99449-275">Used to output custom data types or custom file formats</span></span>

* <span data-ttu-id="99449-276">Procesory zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="99449-276">User-defined processors</span></span>
    * <span data-ttu-id="99449-277">Jeden wiersz i tworzące jeden wiersz</span><span class="sxs-lookup"><span data-stu-id="99449-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="99449-278">Zmniejsz liczbę kolumn lub utworzyć nowe kolumny z wartościami, które pochodzą z istniejącego zestawu kolumn</span><span class="sxs-lookup"><span data-stu-id="99449-278">Used to reduce the number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="99449-279">Appliers zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="99449-279">User-defined appliers</span></span>
    * <span data-ttu-id="99449-280">Jeden wiersz i tworzące 0 do n wierszy</span><span class="sxs-lookup"><span data-stu-id="99449-280">Take one row and produce 0 to n rows</span></span>
    * <span data-ttu-id="99449-281">Używane z Zastosuj zewnętrzne/między</span><span class="sxs-lookup"><span data-stu-id="99449-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="99449-282">Combiners zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="99449-282">User-defined combiners</span></span>
    * <span data-ttu-id="99449-283">Zestawy wierszy — sprzężenia zdefiniowane przez użytkownika łączy</span><span class="sxs-lookup"><span data-stu-id="99449-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="99449-284">Reduktory zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="99449-284">User-defined reducers</span></span>
    * <span data-ttu-id="99449-285">N wierszy i tworzące jeden wiersz</span><span class="sxs-lookup"><span data-stu-id="99449-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="99449-286">Używany do ograniczenia liczby wierszy</span><span class="sxs-lookup"><span data-stu-id="99449-286">Used to reduce the number of rows</span></span>

<span data-ttu-id="99449-287">UDO jest zwykle nazywany jawnie skryptu U-SQL w ramach następujących instrukcji U-SQL:</span><span class="sxs-lookup"><span data-stu-id="99449-287">UDO is typically called explicitly in U-SQL script as part of the following U-SQL statements:</span></span>

* <span data-ttu-id="99449-288">WYODRĘBNIJ</span><span class="sxs-lookup"><span data-stu-id="99449-288">EXTRACT</span></span>
* <span data-ttu-id="99449-289">DANE WYJŚCIOWE</span><span class="sxs-lookup"><span data-stu-id="99449-289">OUTPUT</span></span>
* <span data-ttu-id="99449-290">PROCES</span><span class="sxs-lookup"><span data-stu-id="99449-290">PROCESS</span></span>
* <span data-ttu-id="99449-291">ŁĄCZENIE</span><span class="sxs-lookup"><span data-stu-id="99449-291">COMBINE</span></span>
* <span data-ttu-id="99449-292">ZMNIEJSZ</span><span class="sxs-lookup"><span data-stu-id="99449-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="99449-293">Dla obiektu UDO są ograniczone użycie 0,5 Gb pamięci RAM.</span><span class="sxs-lookup"><span data-stu-id="99449-293">UDO’s are limited to consume 0.5Gb memory.</span></span>  <span data-ttu-id="99449-294">To ograniczenie pamięci nie ma zastosowania do wykonania lokalnego.</span><span class="sxs-lookup"><span data-stu-id="99449-294">This memory limitation does not apply to local executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="99449-295">Użyj ekstraktory zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="99449-295">Use user-defined extractors</span></span>
<span data-ttu-id="99449-296">U-SQL służy do importowania danych zewnętrznych przy użyciu instrukcji WYODRĘBNIANIA.</span><span class="sxs-lookup"><span data-stu-id="99449-296">U-SQL allows you to import external data by using an EXTRACT statement.</span></span> <span data-ttu-id="99449-297">Instrukcja WYODRĘBNIANIA można użyć wbudowanych ekstraktory UDO:</span><span class="sxs-lookup"><span data-stu-id="99449-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="99449-298">*Extractors.Text()*: zapewnia wyodrębniania z plików tekstowych rozdzielanych różnych kodowań.</span><span class="sxs-lookup"><span data-stu-id="99449-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="99449-299">*Extractors.Csv()*: zapewnia wyodrębniania z wartościami rozdzielanymi przecinkami (CSV) plików różnych kodowań.</span><span class="sxs-lookup"><span data-stu-id="99449-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="99449-300">*Extractors.Tsv()*: zapewnia wyodrębniania z wartości tabulatorami (TSV) plików różnych kodowań.</span><span class="sxs-lookup"><span data-stu-id="99449-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="99449-301">Może być przydatne do opracowywania ekstraktor niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="99449-301">It can be useful to develop a custom extractor.</span></span> <span data-ttu-id="99449-302">Może to być przydatne podczas importowania danych, jeśli chcemy wykonaj jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="99449-302">This can be helpful during data import if we want to do any of the following tasks:</span></span>

* <span data-ttu-id="99449-303">Modyfikowanie danych wejściowych podział kolumn i modyfikując poszczególnych wartości.</span><span class="sxs-lookup"><span data-stu-id="99449-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="99449-304">Funkcjonalność PROCESORA jest lepszym rozwiązaniem dla łączenie kolumn.</span><span class="sxs-lookup"><span data-stu-id="99449-304">The PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="99449-305">Przeanalizować danych niestrukturalnych, takich jak strony sieci Web i wiadomości e-mail lub częściowo bez struktury danych, takich jak XML/JSON.</span><span class="sxs-lookup"><span data-stu-id="99449-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="99449-306">Analizować dane przy użyciu kodowania nieobsługiwany.</span><span class="sxs-lookup"><span data-stu-id="99449-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="99449-307">Aby zdefiniować wyodrębniania zdefiniowanych przez użytkownika lub LUCZ, należy utworzyć `IExtractor` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="99449-307">To define a user-defined extractor, or UDE, we need to create an `IExtractor` interface.</span></span> <span data-ttu-id="99449-308">Wszystkie parametry do katalogu, takie jak ogranicznik wiersza/kolumny wejściowe i kodowanie, muszą być zdefiniowane w konstruktorze klasy.</span><span class="sxs-lookup"><span data-stu-id="99449-308">All input parameters to the extractor, such as column/row delimiters, and encoding, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="99449-309">`IExtractor` Interfejsu powinien również zawierać definicji `IEnumerable<IRow>` zastąpienia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="99449-309">The `IExtractor`  interface should also contain a definition for the `IEnumerable<IRow>` override as follows:</span></span>

```
[SqlUserDefinedExtractor]
public class SampleExtractor : IExtractor
{
     public SampleExtractor(string row_delimiter, char col_delimiter)
     { … }

     public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
     { … }
}
```

<span data-ttu-id="99449-310">**SqlUserDefinedExtractor** atrybut wskazuje, że typ powinien zostać zarejestrowany jako ekstraktor zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-310">The **SqlUserDefinedExtractor** attribute indicates that the type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="99449-311">Ta klasa nie może być dziedziczona.</span><span class="sxs-lookup"><span data-stu-id="99449-311">This class cannot be inherited.</span></span>

<span data-ttu-id="99449-312">SqlUserDefinedExtractor jest opcjonalny atrybut LUCZ definicji.</span><span class="sxs-lookup"><span data-stu-id="99449-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="99449-313">Go używać do definiowania właściwości AtomicFileProcessing dla obiekt LUCZ.</span><span class="sxs-lookup"><span data-stu-id="99449-313">It used to define AtomicFileProcessing property for the UDE object.</span></span>

* <span data-ttu-id="99449-314">wartość logiczna AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="99449-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="99449-315">**wartość true,** = wskazuje, że ta ekstraktor wymaga atomic plików wejściowych (JSON, XML,...)</span><span class="sxs-lookup"><span data-stu-id="99449-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="99449-316">**FALSE** = wskazuje, że ten ekstraktor można postępowania w przypadku plików podział / rozproszone (CSV, SEQ,...)</span><span class="sxs-lookup"><span data-stu-id="99449-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="99449-317">Obiekty główne programowania LUCZ **wejściowych** i **dane wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="99449-317">The main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="99449-318">Obiekt wejściowy jest używany do wyliczenia danych wejściowych jako `IUnstructuredReader`.</span><span class="sxs-lookup"><span data-stu-id="99449-318">The input object is used to enumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="99449-319">Obiekt danych wyjściowych jest używany do ustawienia danych wyjściowych w wyniku działania ekstraktor.</span><span class="sxs-lookup"><span data-stu-id="99449-319">The output object is used to set output data as a result of the extractor activity.</span></span>

<span data-ttu-id="99449-320">Dane wejściowe jest dostępny za pośrednictwem `System.IO.Stream` i `System.IO.StreamReader`.</span><span class="sxs-lookup"><span data-stu-id="99449-320">The input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="99449-321">Kolumny wejściowe wyliczenia firma Microsoft najpierw podziału strumienia wejściowego przy użyciu ogranicznik wiersza.</span><span class="sxs-lookup"><span data-stu-id="99449-321">For input columns enumeration, we first split the input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="99449-322">Następnie dodatkowo podzielić wejściowych wiersza części kolumny.</span><span class="sxs-lookup"><span data-stu-id="99449-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="99449-323">Aby ustawić dane wyjściowe, używamy `output.Set` metody.</span><span class="sxs-lookup"><span data-stu-id="99449-323">To set output data, we use the `output.Set` method.</span></span>

<span data-ttu-id="99449-324">Należy zrozumieć, że niestandardowe ekstraktor tylko generuje kolumny i wartości, które są zdefiniowane z danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="99449-324">It's important to understand that the custom extractor only outputs columns and values that are defined with the output.</span></span> <span data-ttu-id="99449-325">Ustaw wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="99449-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="99449-326">Rzeczywiste wyodrębnianie danych wyjściowych jest wyzwalane przez wywołanie metody `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="99449-326">The actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="99449-327">Poniżej przedstawiono przykład ekstraktor:</span><span class="sxs-lookup"><span data-stu-id="99449-327">Following is the extractor example:</span></span>

```
[SqlUserDefinedExtractor(AtomicFileProcessing = true)]
public class FullDescriptionExtractor : IExtractor
{
     private Encoding _encoding;
     private byte[] _row_delim;
     private char _col_delim;

    public FullDescriptionExtractor(Encoding encoding, string row_delim = "\r\n", char col_delim = '\t')
    {
         this._encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
         this._row_delim = this._encoding.GetBytes(row_delim);
         this._col_delim = col_delim;

    }

    public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
    {
         string line;
         //Read the input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split the input by the column delimiter
             string[] parts = line.Split(this._col_delim);
             int count = 0; // start with first column
             foreach (string part in parts)
             {
    if (count == 0)
             {  // for column “guid”, re-generated guid
                 Guid new_guid = Guid.NewGuid();
                 output.Set<Guid>(count, new_guid);
             }
             else if (count == 2)
             {
                 // for column “user”, convert to UPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep the rest of the columns as-is
                 output.Set<string>(count, part);
             }
             count += 1;
             }

         }
         yield return output.AsReadOnly();
         }
         yield break;
     }
}
```

<span data-ttu-id="99449-328">W tym scenariuszu przypadek użycia ekstraktor generuje identyfikator GUID dla kolumny "guid" i konwertuje wartości kolumny "użytkownika" na wielkie litery.</span><span class="sxs-lookup"><span data-stu-id="99449-328">In this use-case scenario, the extractor regenerates the GUID for “guid” column and converts the values of “user” column to upper case.</span></span> <span data-ttu-id="99449-329">Niestandardowe ekstraktory może wygenerować bardziej skomplikowane wyniki analizy danych wejściowych i manipulowanie go.</span><span class="sxs-lookup"><span data-stu-id="99449-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="99449-330">Poniżej przedstawiono podstawowe skryptu U-SQL, który używa ekstraktor niestandardowych:</span><span class="sxs-lookup"><span data-stu-id="99449-330">Following is base U-SQL script that uses a custom extractor:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file
        USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a><span data-ttu-id="99449-331">Użyj outputters zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="99449-331">Use user-defined outputters</span></span>
<span data-ttu-id="99449-332">Zdefiniowane przez użytkownika outputter jest innego obiektu UDO U-SQL, który umożliwia rozszerzanie wbudowanej funkcji U-SQL.</span><span class="sxs-lookup"><span data-stu-id="99449-332">User-defined outputter is another U-SQL UDO that allows you to extend built-in U-SQL functionality.</span></span> <span data-ttu-id="99449-333">Podobnie jak wyodrębnianie, istnieje kilka wbudowanych outputters.</span><span class="sxs-lookup"><span data-stu-id="99449-333">Similar to the extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="99449-334">*Outputters.Text()*: zapisuje dane w plikach tekstowych rozdzielanych różnych kodowań.</span><span class="sxs-lookup"><span data-stu-id="99449-334">*Outputters.Text()*: Writes data to delimited text files of different encodings.</span></span>
* <span data-ttu-id="99449-335">*Outputters.Csv()*: zapisuje dane do plików różnych kodowań plik wartości rozdzielanych przecinkami (CSV).</span><span class="sxs-lookup"><span data-stu-id="99449-335">*Outputters.Csv()*: Writes data to comma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="99449-336">*Outputters.Tsv()*: zapisuje dane do plików różnych kodowań wartość tabulatorami (TSV).</span><span class="sxs-lookup"><span data-stu-id="99449-336">*Outputters.Tsv()*: Writes data to tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="99449-337">Niestandardowe outputter pozwala na zapis danych w niestandardowym formacie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="99449-337">Custom outputter allows you to write data in a custom defined format.</span></span> <span data-ttu-id="99449-338">Może to być przydatne w przypadku następujących zadań:</span><span class="sxs-lookup"><span data-stu-id="99449-338">This can be useful for the following tasks:</span></span>

* <span data-ttu-id="99449-339">Zapisywanie danych w plikach częściową strukturą lub bez struktury.</span><span class="sxs-lookup"><span data-stu-id="99449-339">Writing data to semi-structured or unstructured files.</span></span>
* <span data-ttu-id="99449-340">Zapisywanie danych nie obsługuje kodowania.</span><span class="sxs-lookup"><span data-stu-id="99449-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="99449-341">Modyfikowanie danych wyjściowych lub dodanie atrybutów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="99449-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="99449-342">Aby zdefiniować outputter zdefiniowane przez użytkownika, należy utworzyć `IOutputter` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="99449-342">To define user-defined outputter, we need to create the `IOutputter` interface.</span></span>

<span data-ttu-id="99449-343">Poniżej znajduje się podstawowym `IOutputter` Implementacja klasy:</span><span class="sxs-lookup"><span data-stu-id="99449-343">Following is the base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="99449-344">Wszystkie parametry wejściowe outputter, takich jak ogranicznik wiersza/kolumny, kodowanie i tak dalej, muszą być zdefiniowane w konstruktorze klasy.</span><span class="sxs-lookup"><span data-stu-id="99449-344">All input parameters to the outputter, such as column/row delimiters, encoding, and so on, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="99449-345">`IOutputter` Interfejsu powinien również zawierać definicji `void Output` zastąpienia.</span><span class="sxs-lookup"><span data-stu-id="99449-345">The `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="99449-346">Atrybut `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` Opcjonalnie można ustawić dla przetwarzania plików atomic.</span><span class="sxs-lookup"><span data-stu-id="99449-346">The attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="99449-347">Aby uzyskać więcej informacji zobacz następujące informacje.</span><span class="sxs-lookup"><span data-stu-id="99449-347">For more information, see the following details.</span></span>

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class MyOutputter : IOutputter
{

    public MyOutputter(myparam1, myparam2)
    {
      …
    }

    public override void Close()
    {
      …
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
      …
    }
}
```

* <span data-ttu-id="99449-348">`Output`jest wywoływana dla każdego wiersza wejściowego.</span><span class="sxs-lookup"><span data-stu-id="99449-348">`Output` is called for each input row.</span></span> <span data-ttu-id="99449-349">Zwraca `IUnstructuredWriter output` zestawu wierszy.</span><span class="sxs-lookup"><span data-stu-id="99449-349">It returns the `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="99449-350">Konstruktor klasy jest używany do przekazania parametrów do outputter zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-350">The Constructor class is used to pass parameters to the user-defined outputter.</span></span>
* <span data-ttu-id="99449-351">`Close`Służy do zastępowania opcjonalnie kosztowne stanu wersji lub określić, kiedy ostatni wiersz został zapisany.</span><span class="sxs-lookup"><span data-stu-id="99449-351">`Close` is used to optionally override to release expensive state or determine when the last row was written.</span></span>

<span data-ttu-id="99449-352">**SqlUserDefinedOutputter** atrybut wskazuje, że typ powinien zostać zarejestrowany jako outputter zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-352">**SqlUserDefinedOutputter** attribute indicates that the type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="99449-353">Ta klasa nie może być dziedziczona.</span><span class="sxs-lookup"><span data-stu-id="99449-353">This class cannot be inherited.</span></span>

<span data-ttu-id="99449-354">SqlUserDefinedOutputter jest opcjonalny atrybut dla definicji outputter zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="99449-355">Służy do definiowania właściwości AtomicFileProcessing.</span><span class="sxs-lookup"><span data-stu-id="99449-355">It's used to define the AtomicFileProcessing property.</span></span>

* <span data-ttu-id="99449-356">wartość logiczna AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="99449-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="99449-357">**wartość true,** = wskazuje, że ten outputter wymaga pliki wyjściowe niepodzielne (JSON, XML,...)</span><span class="sxs-lookup"><span data-stu-id="99449-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="99449-358">**FALSE** = wskazuje, że ten outputter można postępowania w przypadku plików podział / rozproszone (CSV, SEQ,...)</span><span class="sxs-lookup"><span data-stu-id="99449-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="99449-359">Obiekty główne programowania są **wiersza** i **dane wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="99449-359">The main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="99449-360">**Wiersza** obiekt jest używany do wyliczenia dane wyjściowe jako `IRow` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="99449-360">The **row** object is used to enumerate output data as `IRow` interface.</span></span> <span data-ttu-id="99449-361">**Dane wyjściowe** służy do ustawiania dane wyjściowe do pliku docelowego.</span><span class="sxs-lookup"><span data-stu-id="99449-361">**Output** is used to set output data to the target file.</span></span>

<span data-ttu-id="99449-362">Danych wyjściowych jest dostępny za pośrednictwem `IRow` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="99449-362">The output data is accessed through the `IRow` interface.</span></span> <span data-ttu-id="99449-363">Dane wyjściowe są przekazywane wiersza w czasie.</span><span class="sxs-lookup"><span data-stu-id="99449-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="99449-364">Poszczególne wartości wyliczane są przez wywołanie metody Get interfejsu IRow:</span><span class="sxs-lookup"><span data-stu-id="99449-364">The individual values are enumerated by calling the Get method of the IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="99449-365">Można ustalić nazwy poszczególnych kolumn przez wywołanie metody `row.Schema`:</span><span class="sxs-lookup"><span data-stu-id="99449-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="99449-366">Takie podejście umożliwia tworzenie elastycznych outputter dla żadnego schematu metadanych.</span><span class="sxs-lookup"><span data-stu-id="99449-366">This approach enables you to build a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="99449-367">Dane są zapisywane do pliku przy użyciu `System.IO.StreamWriter`.</span><span class="sxs-lookup"><span data-stu-id="99449-367">The output data is written to file by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="99449-368">Parametr strumienia jest ustawiony na `output.BaseStrea` jako część `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="99449-368">The stream parameter is set to `output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="99449-369">Należy pamiętać, że ważne jest, aby opróżnić buforu danych do pliku po każdej iteracji wiersza.</span><span class="sxs-lookup"><span data-stu-id="99449-369">Note that it's important to flush the data buffer to the file after each row iteration.</span></span> <span data-ttu-id="99449-370">Ponadto `StreamWriter` z atrybutu jednorazowe włączone (ustawienie domyślne) i można użyć obiektu **przy użyciu** — słowo kluczowe:</span><span class="sxs-lookup"><span data-stu-id="99449-370">In addition, the `StreamWriter` object must be used with the Disposable attribute enabled (default) and with the **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="99449-371">W przeciwnym razie wywołanie metody Flush() jawnie po każdej iteracji.</span><span class="sxs-lookup"><span data-stu-id="99449-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="99449-372">Ten zostanie przedstawiony w następującym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="99449-372">We show this in the following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="99449-373">Ustaw nagłówki i stopki dla outputter zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="99449-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="99449-374">Aby ustawić nagłówka, należy użyć przepływu wykonywania iteracji jednego.</span><span class="sxs-lookup"><span data-stu-id="99449-374">To set a header, use single iteration execution flow.</span></span>

```
public override void Output(IRow row, IUnstructuredWriter output)
{
 …
if (isHeaderRow)
{
    …                
}

 …
if (isHeaderRow)
{
    isHeaderRow = false;
}
 …
}
}
```

<span data-ttu-id="99449-375">Kod w pierwszym `if (isHeaderRow)` bloku jest wykonywane tylko raz.</span><span class="sxs-lookup"><span data-stu-id="99449-375">The code in the first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="99449-376">Stopki, użyj odwołania do wystąpienia `System.IO.Stream` obiektu (`output.BaseStream`).</span><span class="sxs-lookup"><span data-stu-id="99449-376">For the footer, use the reference to the instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="99449-377">Zapisywanie stopki w metody Close() `IOutputter` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="99449-377">Write the footer in the Close() method of the `IOutputter` interface.</span></span>  <span data-ttu-id="99449-378">(Aby uzyskać więcej informacji, zobacz poniższy przykład).</span><span class="sxs-lookup"><span data-stu-id="99449-378">(For more information, see the following example.)</span></span>

<span data-ttu-id="99449-379">Poniżej przedstawiono przykład outputter zdefiniowane przez użytkownika:</span><span class="sxs-lookup"><span data-stu-id="99449-379">Following is an example of a user-defined outputter:</span></span>

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class HTMLOutputter : IOutputter
{
    // Local variables initialization
    private string row_delimiter;
    private char col_delimiter;
    private bool isHeaderRow;
    private Encoding encoding;
    private bool IsTableHeader = true;
    private Stream g_writer;

    // Parameters definition            
    public HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    this.isHeaderRow = isHeader;
    this.encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
    }

    // The Close method is used to write the footer to the file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference to IO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization to enumerate column names
    ISchema schema = row.Schema;

    // This is a data-independent header--HTML table definition
    if (IsTableHeader)
    {
        streamWriter.Write("<table border=1>");
        IsTableHeader = false;
    }

    // HTML table attributes
    string header_wrapper_on = "<th>";
    string header_wrapper_off = "</th>";
    string data_wrapper_on = "<td>";
    string data_wrapper_off = "</td>";

    // Header row output--runs only once
    if (isHeaderRow)
    {
        streamWriter.Write("<tr>");
        for (int i = 0; i < schema.Count(); i++)
        {
        var col = schema[i];
        streamWriter.Write(header_wrapper_on + col.Name + header_wrapper_off);
        }
        streamWriter.Write("</tr>");
    }

    // Data row output
    streamWriter.Write("<tr>");                
    for (int i = 0; i < schema.Count(); i++)
    {
        var col = schema[i];
        string val = "";
        try
        {
        // Data type enumeration--required to match the distinct list of types from OUTPUT statement
        switch (col.Type.Name.ToString().ToLower())
        {
            case "string": val = row.Get<string>(col.Name).ToString(); break;
            case "guid": val = row.Get<Guid>(col.Name).ToString(); break;
            default: break;
        }
        }
        // Handling NULL values--keeping them empty
        catch (System.NullReferenceException)
        {
        }
        streamWriter.Write(data_wrapper_on + val + data_wrapper_off);
    }
    streamWriter.Write("</tr>");

    if (isHeaderRow)
    {
        isHeaderRow = false;
    }
    // Reference to the instance of the IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define the factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

<span data-ttu-id="99449-380">I podstawowy skrypt U-SQL:</span><span class="sxs-lookup"><span data-stu-id="99449-380">And U-SQL base script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.html";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
         FROM @input_file
         USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 
    TO @output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="99449-381">Jest to outputter HTML, który tworzy plik HTML z danych tabeli.</span><span class="sxs-lookup"><span data-stu-id="99449-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="99449-382">Wywołanie outputter z podstawowej skryptu U-SQL</span><span class="sxs-lookup"><span data-stu-id="99449-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="99449-383">Aby wywołać outputter niestandardowych z podstawowej skryptu U-SQL, nowe wystąpienie obiektu outputter musi być utworzony.</span><span class="sxs-lookup"><span data-stu-id="99449-383">To call a custom outputter from the base U-SQL script, the new instance of the outputter object has to be created.</span></span>

```sql
OUTPUT @rs0 TO @output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="99449-384">Aby uniknąć tworzenia wystąpienia obiektu w skrypcie podstawowej, można utworzyć otoki funkcji, jak pokazano w naszym przykładzie wcześniej:</span><span class="sxs-lookup"><span data-stu-id="99449-384">To avoid creating an instance of the object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

```c#
        // Define the factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

<span data-ttu-id="99449-385">W takim przypadku wywołania oryginalnego wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="99449-385">In this case, the original call looks like the following:</span></span>

```
OUTPUT @rs0 
TO @output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="99449-386">Używają procesorów zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="99449-386">Use user-defined processors</span></span>
<span data-ttu-id="99449-387">Procesor zdefiniowane przez użytkownika lub UDP, jest typem obiektu UDO U-SQL, który umożliwia przetwarzanie przychodzących wierszy, stosując funkcje programowania.</span><span class="sxs-lookup"><span data-stu-id="99449-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you to process the incoming rows by applying programmability features.</span></span> <span data-ttu-id="99449-388">UDP umożliwia łączenie kolumn, zmodyfikuj wartości, a w razie potrzeby należy dodać nowe kolumny.</span><span class="sxs-lookup"><span data-stu-id="99449-388">UDP enables you to combine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="99449-389">Zasadniczo pomaga przetworzyć zestawu wierszy do tworzenia wymaganych elementów danych.</span><span class="sxs-lookup"><span data-stu-id="99449-389">Basically, it helps to process a rowset to produce required data elements.</span></span>

<span data-ttu-id="99449-390">Aby zdefiniować UDP, należy utworzyć `IProcessor` interfejsu z `SqlUserDefinedProcessor` atrybut, który jest opcjonalne dla protokołu UDP.</span><span class="sxs-lookup"><span data-stu-id="99449-390">To define a UDP, we need to create an `IProcessor` interface with the `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="99449-391">Ten interfejs musi zawierać definicję dla `IRow` zastąpić interfejsu zestawu wierszy, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="99449-391">This interface should contain the definition for the `IRow` interface rowset override, as shown in the following example:</span></span>

```
[SqlUserDefinedProcessor]
public class MyProcessor: IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
        …
 }
}
```

<span data-ttu-id="99449-392">**SqlUserDefinedProcessor** wskazuje, że typ powinien być zarejestrowany jako procesor zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-392">**SqlUserDefinedProcessor** indicates that the type should be registered as a user-defined processor.</span></span> <span data-ttu-id="99449-393">Ta klasa nie może być dziedziczona.</span><span class="sxs-lookup"><span data-stu-id="99449-393">This class cannot be inherited.</span></span>

<span data-ttu-id="99449-394">Atrybut SqlUserDefinedProcessor jest **opcjonalne** dla definicji UDP.</span><span class="sxs-lookup"><span data-stu-id="99449-394">The SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="99449-395">Obiekty główne programowania są **wejściowych** i **dane wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="99449-395">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="99449-396">Obiekt wejściowy służy do wyliczenia kolumny wejściowe i wyjściowe oraz ustawić dane wyjściowe w wyniku aktywności procesora.</span><span class="sxs-lookup"><span data-stu-id="99449-396">The input object is used to enumerate input columns and output, and to set output data as a result of the processor activity.</span></span>

<span data-ttu-id="99449-397">Wyliczenia kolumny wejściowe używamy `input.Get` metody.</span><span class="sxs-lookup"><span data-stu-id="99449-397">For input columns enumeration, we use the `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="99449-398">Parametr `input.Get` metody jest przekazywany jako część kolumny `PRODUCE` klauzuli `PROCESS` instrukcji podstawowy skrypt U-SQL.</span><span class="sxs-lookup"><span data-stu-id="99449-398">The parameter for `input.Get` method is a column that's passed as part of the `PRODUCE` clause of the `PROCESS` statement of the U-SQL base script.</span></span> <span data-ttu-id="99449-399">Należy użyć prawidłowy typ danych w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="99449-399">We need to use the correct data type here.</span></span>

<span data-ttu-id="99449-400">Dla danych wyjściowych, użyj `output.Set` metody.</span><span class="sxs-lookup"><span data-stu-id="99449-400">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="99449-401">Należy pamiętać, że niestandardowe producentów wyświetla tylko kolumny i wartości, które są zdefiniowane z `output.Set` wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="99449-401">It's important to note that custom producer only outputs columns and values that are defined with the `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="99449-402">Procesor rzeczywiste dane wyjściowe zostanie wywołany przez wywołanie metody `return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="99449-402">The actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="99449-403">Poniżej przedstawiono przykład procesora:</span><span class="sxs-lookup"><span data-stu-id="99449-403">Following is a processor example:</span></span>

```
[SqlUserDefinedProcessor]
public class FullDescriptionProcessor : IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
     string user = input.Get<string>("user");
     string des = input.Get<string>("des");
     string full_description = user.ToUpper() + "=>" + des;
     output.Set<string>("dt", input.Get<string>("dt"));
     output.Set<string>("full_description", full_description);
     output.Set<Guid>("new_guid", Guid.NewGuid());
     output.Set<Guid>("guid", input.Get<Guid>("guid"));
     return output.AsReadOnly();
 }
}
```

<span data-ttu-id="99449-404">W tym scenariuszu przypadek użycia procesora generuje nową kolumnę o nazwie "full_description" łącząc istniejące kolumny — w tym przypadku "użytkownika" wielkimi literami i "des".</span><span class="sxs-lookup"><span data-stu-id="99449-404">In this use-case scenario, the processor is generating a new column called “full_description” by combining the existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="99449-405">Również generuje identyfikator GUID i zwraca oryginalnego i nowej wartości identyfikatora GUID.</span><span class="sxs-lookup"><span data-stu-id="99449-405">It also regenerates a GUID and returns the original and new GUID values.</span></span>

<span data-ttu-id="99449-406">Jak widać w poprzednim przykładzie, należy wywołać metodę C# podczas `output.Set` wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="99449-406">As you can see from the previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="99449-407">Poniżej przedstawiono przykład podstawowego skryptu U-SQL, który używa niestandardowego procesora:</span><span class="sxs-lookup"><span data-stu-id="99449-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
     PROCESS @rs0
     PRODUCE dt String,
             full_description String,
             guid Guid,
             new_guid Guid
     USING new USQL_Programmability.FullDescriptionProcessor();

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a><span data-ttu-id="99449-408">Użyj appliers zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="99449-408">Use user-defined appliers</span></span>
<span data-ttu-id="99449-409">Zdefiniowane przez użytkownika applier U-SQL umożliwia wywołanie niestandardowej funkcji języka C# dla każdego wiersza, który jest zwracany przez wyrażenie Tabela zewnętrzna zapytania.</span><span class="sxs-lookup"><span data-stu-id="99449-409">A U-SQL user-defined applier enables you to invoke a custom C# function for each row that's returned by the outer table expression of a query.</span></span> <span data-ttu-id="99449-410">Odpowiednie dane wejściowe jest obliczane dla każdego wiersza wejściowego po lewej stronie, a wiersze, które są tworzone są łączone na ostateczne dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="99449-410">The right input is evaluated for each row from the left input, and the rows that are produced are combined for the final output.</span></span> <span data-ttu-id="99449-411">Lista kolumn, które są tworzone przez operatora APPLY są kombinacją zestawu kolumn w lewej i prawej danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="99449-411">The list of columns that are produced by the APPLY operator are the combination of the set of columns in the left and the right input.</span></span>

<span data-ttu-id="99449-412">Zdefiniowane przez użytkownika applier jest wywoływany jako część wyrażenia USQL wybierz.</span><span class="sxs-lookup"><span data-stu-id="99449-412">User-defined applier is being invoked as part of the USQL SELECT expression.</span></span>

<span data-ttu-id="99449-413">Typowy wywołanie applier użytkownika wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="99449-413">The typical call to the user-defined applier looks like the following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used to pass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="99449-414">Aby uzyskać więcej informacji o używaniu appliers w wyrażeniu SELECT, zobacz [U-SQL wybierz wybrać między Zastosuj i zewnętrzne](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span><span class="sxs-lookup"><span data-stu-id="99449-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="99449-415">Zdefiniowane przez użytkownika definicji klasy podstawowej applier wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="99449-415">The user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="99449-416">Aby zdefiniować applier zdefiniowane przez użytkownika, należy utworzyć `IApplier` interfejsu z [`SqlUserDefinedApplier`] atrybut, który jest opcjonalne dla definicji applier zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-416">To define a user-defined applier, we need to create the `IApplier` interface with the [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
    public ParserApplier()
    {
        …
    }

    public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
    {
        …
    }
}
```

* <span data-ttu-id="99449-417">Zastosuj jest wywoływana dla każdego wiersza tabeli zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="99449-417">Apply is called for each row of the outer table.</span></span> <span data-ttu-id="99449-418">Zwraca `IUpdatableRow` output zestawu wierszy.</span><span class="sxs-lookup"><span data-stu-id="99449-418">It returns the `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="99449-419">Konstruktor klasy jest używany do przekazania parametrów do applier zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-419">The Constructor class is used to pass parameters to the user-defined applier.</span></span>

<span data-ttu-id="99449-420">**SqlUserDefinedApplier** wskazuje, że typ powinien zostać zarejestrowany jako applier zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-420">**SqlUserDefinedApplier** indicates that the type should be registered as a user-defined applier.</span></span> <span data-ttu-id="99449-421">Ta klasa nie może być dziedziczona.</span><span class="sxs-lookup"><span data-stu-id="99449-421">This class cannot be inherited.</span></span>

<span data-ttu-id="99449-422">**SqlUserDefinedApplier** jest **opcjonalne** dla definicji applier zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="99449-423">Obiekty główne programowania znajdują się w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="99449-423">The main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="99449-424">Wejściowe zestawy wierszy są przekazywane jako `IRow` wejściowego.</span><span class="sxs-lookup"><span data-stu-id="99449-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="99449-425">Wiersze dane wyjściowe są generowane jako `IUpdatableRow` interfejsu danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="99449-425">The output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="99449-426">Można ustalić nazwy poszczególnych kolumn przez wywołanie metody `IRow` metody schematu.</span><span class="sxs-lookup"><span data-stu-id="99449-426">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="99449-427">Aby uzyskać rzeczywiste dane z przychodzącego `IRow`, możemy użyć metody Get() `IRow` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="99449-427">To get the actual data values from the incoming `IRow`, we use the Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="99449-428">Lub używamy nazwy kolumn schematu:</span><span class="sxs-lookup"><span data-stu-id="99449-428">Or we use the schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="99449-429">Należy ustawić wartości danych wyjściowych z `IUpdatableRow` danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="99449-429">The output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="99449-430">Ważne jest, aby zrozumieć, że niestandardowe appliers output tylko kolumny i wartości, które są zdefiniowane z `output.Set` wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="99449-430">It is important to understand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="99449-431">Rzeczywiste dane wyjściowe zostanie wywołany przez wywołanie metody `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="99449-431">The actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="99449-432">Parametry applier zdefiniowane przez użytkownika mogą być przekazywane do konstruktora.</span><span class="sxs-lookup"><span data-stu-id="99449-432">The user-defined applier parameters can be passed to the constructor.</span></span> <span data-ttu-id="99449-433">Applier może zwracać zmienną liczbę kolumn, które muszą zostać zdefiniowane podczas wywołania applier w podstawowej skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="99449-433">Applier can return a variable number of columns that need to be defined during the applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="99449-434">Oto przykład applier zdefiniowane przez użytkownika:</span><span class="sxs-lookup"><span data-stu-id="99449-434">Here is the user-defined applier example:</span></span>

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
private string parsingPart;

public ParserApplier(string parsingPart)
{
    if (parsingPart.ToUpper().Contains("ALL")
    || parsingPart.ToUpper().Contains("MAKE")
    || parsingPart.ToUpper().Contains("MODEL")
    || parsingPart.ToUpper().Contains("YEAR")
    || parsingPart.ToUpper().Contains("TYPE")
    || parsingPart.ToUpper().Contains("MILLAGE")
    )
    {
    this.parsingPart = parsingPart;
    }
    else
    {
    throw new ArgumentException("Incorrect parameter. Please use: 'ALL[MAKE|MODEL|TYPE|MILLAGE]'");
    }
}

public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
{

    string[] properties = input.Get<string>("properties").Split(',');

    //  only process with correct number of properties
    if (properties.Count() == 5)
    {

    string make = properties[0];
    string model = properties[1];
    string year = properties[2];
    string type = properties[3];
    int millage = -1;

    // Only return millage if it is number, otherwise, -1
    if (!int.TryParse(properties[4], out millage))
    {
        millage = -1;
    }

    if (parsingPart.ToUpper().Contains("MAKE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("make", make);
    if (parsingPart.ToUpper().Contains("MODEL") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("model", model);
    if (parsingPart.ToUpper().Contains("YEAR") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("year", year);
    if (parsingPart.ToUpper().Contains("TYPE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("type", type);
    if (parsingPart.ToUpper().Contains("MILLAGE") || parsingPart.ToUpper().Contains("ALL")) output.Set<int>("millage", millage);
    }
    yield return output.AsReadOnly();            
}
}
```

<span data-ttu-id="99449-435">Poniżej przedstawiono podstawowe skryptu U-SQL dla tego użytkownika applier:</span><span class="sxs-lookup"><span data-stu-id="99449-435">Following is the base U-SQL script for this user-defined applier:</span></span>

```
DECLARE @input_file string = @"c:\usql-programmability\car_fleet.tsv";
DECLARE @output_file string = @"c:\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        stocknumber int,
        vin String,
        properties String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT
        r.stocknumber,
        r.vin,
        properties.make,
        properties.model,
        properties.year,
        properties.type,
        properties.millage
    FROM @rs0 AS r
    CROSS APPLY
    new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="99449-436">W tym scenariuszu przypadków użycia applier zdefiniowane przez użytkownika działa jako wartości rozdzielane przecinkami analizatora składni właściwości floty samochodów.</span><span class="sxs-lookup"><span data-stu-id="99449-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for the car fleet properties.</span></span> <span data-ttu-id="99449-437">Wiersze pliku wejściowego wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="99449-437">The input file rows look like the following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="99449-438">Jest to typowe tabulacji TSV plik z kolumną właściwości zawierającego właściwości samochodu, takich jak marka i model.</span><span class="sxs-lookup"><span data-stu-id="99449-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="99449-439">Te właściwości należy przeanalizować do kolumn tabeli.</span><span class="sxs-lookup"><span data-stu-id="99449-439">Those properties must be parsed to the table columns.</span></span> <span data-ttu-id="99449-440">Applier, który został dostarczony umożliwia także wygenerować dynamiczne liczba właściwości w zestawie wierszy wyników, na podstawie parametru, który jest przekazywany.</span><span class="sxs-lookup"><span data-stu-id="99449-440">The applier that's provided also enables you to generate a dynamic number of properties in the result rowset, based on the parameter that's passed.</span></span> <span data-ttu-id="99449-441">Można wygenerować właściwości wszystkich lub określonych tylko właściwości.</span><span class="sxs-lookup"><span data-stu-id="99449-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="99449-442">Zdefiniowane przez użytkownika applier można wywołać jako nowe wystąpienie obiektu applier:</span><span class="sxs-lookup"><span data-stu-id="99449-442">The user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="99449-443">Lub wywołanie metody fabryki otoki:</span><span class="sxs-lookup"><span data-stu-id="99449-443">Or with the invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="99449-444">Użyj combiners zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="99449-444">Use user-defined combiners</span></span>
<span data-ttu-id="99449-445">Zdefiniowane przez użytkownika łączenia lub UDC, umożliwia połączenie wiersze z lewego i prawego zestawów wierszy, opartych na logice niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="99449-445">User-defined combiner, or UDC, enables you to combine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="99449-446">Zdefiniowane przez użytkownika łączenia jest używany z łączenia wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="99449-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="99449-447">Łączenia jest wywoływany z wyrażeniem łączenia, który dostarcza niezbędne informacje o zarówno wejściowe zestawy wierszy, kolumny grupowania, oczekiwany wynik schematu i dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="99449-447">A combiner is being invoked with the COMBINE expression that provides the necessary information about both the input rowsets, the grouping columns, the expected result schema, and additional information.</span></span>

<span data-ttu-id="99449-448">Aby wywołać łączenia w podstawowej skryptu U-SQL, możemy użyć następującej składni:</span><span class="sxs-lookup"><span data-stu-id="99449-448">To call a combiner in a base U-SQL script, we use the following syntax:</span></span>

```
Combine_Expression :=
    'COMBINE' Combine_Input
    'WITH' Combine_Input
    Join_On_Clause
    Produce_Clause
    [Readonly_Clause]
    [Required_Clause]
    USING_Clause.
```

<span data-ttu-id="99449-449">Aby uzyskać więcej informacji, zobacz [łączenia wyrażenia (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span><span class="sxs-lookup"><span data-stu-id="99449-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="99449-450">Aby zdefiniować łączenia zdefiniowane przez użytkownika, należy utworzyć `ICombiner` interfejsu z [`SqlUserDefinedCombiner`] atrybut, który jest opcjonalne dla definicji łączenia zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-450">To define a user-defined combiner, we need to create the `ICombiner` interface with the [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="99449-451">Podstawa `ICombiner` definicji klasy:</span><span class="sxs-lookup"><span data-stu-id="99449-451">Base `ICombiner` class definition:</span></span>

```
public abstract class ICombiner : IUserDefinedOperator
{
protected ICombiner();
public virtual IEnumerable<IRow> Combine(List<IRowset> inputs,
       IUpdatableRow output);
public abstract IEnumerable<IRow> Combine(IRowset left, IRowset right,
       IUpdatableRow output);
}
```

<span data-ttu-id="99449-452">Implementacji niestandardowego `ICombiner` interfejsu powinny zawierać definicji `IEnumerable<IRow>` połączyć zastąpienia.</span><span class="sxs-lookup"><span data-stu-id="99449-452">The custom implementation of an `ICombiner` interface should contain the definition for an `IEnumerable<IRow>` Combine override.</span></span>

```
[SqlUserDefinedCombiner]
public class MyCombiner : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    …
}
}
```

<span data-ttu-id="99449-453">**SqlUserDefinedCombiner** atrybut wskazuje, że typ powinien zostać zarejestrowany jako łączenia zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-453">The **SqlUserDefinedCombiner** attribute indicates that the type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="99449-454">Ta klasa nie może być dziedziczona.</span><span class="sxs-lookup"><span data-stu-id="99449-454">This class cannot be inherited.</span></span>

<span data-ttu-id="99449-455">**SqlUserDefinedCombiner** służy do definiowania właściwości trybie łączenia.</span><span class="sxs-lookup"><span data-stu-id="99449-455">**SqlUserDefinedCombiner** is used to define the Combiner mode property.</span></span> <span data-ttu-id="99449-456">Jest opcjonalny atrybut dla definicji łączenia zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="99449-457">Tryb CombinerMode</span><span class="sxs-lookup"><span data-stu-id="99449-457">CombinerMode     Mode</span></span>

<span data-ttu-id="99449-458">Wyliczenia CombinerMode może przyjmować następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="99449-458">CombinerMode enum can take the following values:</span></span>

* <span data-ttu-id="99449-459">Pełny (0), każdy wiersz danych wyjściowych zależy od potencjalnie wszystkie wiersze danych wejściowych od lewej i prawej z taką samą wartość klucza.</span><span class="sxs-lookup"><span data-stu-id="99449-459">Full  (0) Every output row potentially depends on all the input rows from left and right       with the same key value.</span></span>

* <span data-ttu-id="99449-460">Od lewej (1) każdy wiersz danych wyjściowych jest zależna od pojedynczy wiersz wejściowych z lewej strony (i potencjalnie wszystkie wiersze z prawej strony, z taką samą wartość klucza).</span><span class="sxs-lookup"><span data-stu-id="99449-460">Left  (1) Every output row depends on a single input row from the left (and potentially all rows       from the right with the same key value).</span></span>

* <span data-ttu-id="99449-461">Prawo każdego wiersza danych wyjściowych jest zależna od pojedynczy wiersz wejściowych z prawej (i potencjalnie wszystkie wiersze z lewej strony o tej samej wartości klucza) (2).</span><span class="sxs-lookup"><span data-stu-id="99449-461">Right (2)     Every output row depends on a single input row from the right (and potentially all rows       from the left with the same key value).</span></span>

* <span data-ttu-id="99449-462">Wewnętrzna (3) w pojedynczym wierszu wejściowego w lewo i prawo z taką samą wartość zależy od każdego wiersza danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="99449-462">Inner (3) Every output row depends on a single input row from left and right with the same value.</span></span>

<span data-ttu-id="99449-463">Przykład: [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="99449-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="99449-464">Obiekty główne programowania są:</span><span class="sxs-lookup"><span data-stu-id="99449-464">The main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="99449-465">Wejściowe zestawy wierszy są przekazywane jako **po lewej stronie** i **prawo** `IRowset` typ interfejsu.</span><span class="sxs-lookup"><span data-stu-id="99449-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="99449-466">Oba zestawy wierszy musi zostać wyliczone do przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="99449-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="99449-467">Można tylko wyliczyć każdy interfejs, a więc musimy wyliczyć i jego pamięci podręcznej, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="99449-467">You can only enumerate each interface once, so we have to enumerate and cache it if necessary.</span></span>

<span data-ttu-id="99449-468">Na potrzeby buforowania, można utworzyć listy\<T\> typ konstrukcji pamięci w związku z tym składnika LINQ wykonywanie zapytania, w szczególności listę <`IRow`>.</span><span class="sxs-lookup"><span data-stu-id="99449-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="99449-469">Typ anonimowy danych może służyć podczas wyliczania również.</span><span class="sxs-lookup"><span data-stu-id="99449-469">The anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="99449-470">Zobacz [wprowadzenie do kwerend LINQ (C#)](https://msdn.microsoft.com/library/bb397906.aspx) uzyskać więcej informacji dotyczących zapytań LINQ i [IEnumerable\<T\> interfejsu](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) Aby uzyskać więcej informacji na temat interfejsu IEnumerable\<T\> interfejsu.</span><span class="sxs-lookup"><span data-stu-id="99449-470">See [Introduction to LINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="99449-471">Aby uzyskać rzeczywiste dane z przychodzącego `IRowset`, możemy użyć metody Get() `IRow` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="99449-471">To get the actual data values from the incoming `IRowset`, we use the Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="99449-472">Można ustalić nazwy poszczególnych kolumn przez wywołanie metody `IRow` metody schematu.</span><span class="sxs-lookup"><span data-stu-id="99449-472">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="99449-473">Lub przy użyciu nazwy kolumn schematu:</span><span class="sxs-lookup"><span data-stu-id="99449-473">Or by using the schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="99449-474">Ogólne wyliczenia za pomocą LINQ wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="99449-474">The general enumeration with LINQ looks like the following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="99449-475">Po wyliczania oba zestawy wierszy, zamierzamy pętli wszystkich wierszy.</span><span class="sxs-lookup"><span data-stu-id="99449-475">After enumerating both rowsets, we are going to loop through all rows.</span></span> <span data-ttu-id="99449-476">Dla każdego wiersza w zestawie wierszy po lewej stronie zamierzamy Znajdź wszystkie wiersze, które spełniają warunek naszych łączenia.</span><span class="sxs-lookup"><span data-stu-id="99449-476">For each row in the left rowset, we are going to find all rows that satisfy the condition of our combiner.</span></span>

<span data-ttu-id="99449-477">Należy ustawić wartości danych wyjściowych z `IUpdatableRow` danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="99449-477">The output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="99449-478">Rzeczywiste wyniki jest wyzwalany przez wywołanie do `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="99449-478">The actual output is triggered by calling to `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="99449-479">Poniżej przedstawiono przykład łączenia:</span><span class="sxs-lookup"><span data-stu-id="99449-479">Following is a combiner example:</span></span>

```
[SqlUserDefinedCombiner]
public class CombineSales : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    var internetSales =
    (from row in left.Rows
          select new
          {
              ProductKey = row.Get<int>("ProductKey"),
              OrderDateKey = row.Get<int>("OrderDateKey"),
              SalesAmount = row.Get<decimal>("SalesAmount"),
              TaxAmt = row.Get<decimal>("TaxAmt")
          }).ToList();

    var resellerSales =
    (from row in right.Rows
     select new
     {
     ProductKey = row.Get<int>("ProductKey"),
     OrderDateKey = row.Get<int>("OrderDateKey"),
     SalesAmount = row.Get<decimal>("SalesAmount"),
     TaxAmt = row.Get<decimal>("TaxAmt")
     }).ToList();

    foreach (var row_i in internetSales)
    {
    foreach (var row_r in resellerSales)
    {

        if (
        row_i.OrderDateKey > 0
        && row_i.OrderDateKey < row_r.OrderDateKey
        && row_i.OrderDateKey == 20010701
        && (row_r.SalesAmount + row_r.TaxAmt) > 20000)
        {
        output.Set<int>("OrderDateKey", row_i.OrderDateKey);
        output.Set<int>("ProductKey", row_i.ProductKey);
        output.Set<decimal>("Internet_Sales_Amount", row_i.SalesAmount + row_i.TaxAmt);
        output.Set<decimal>("Reseller_Sales_Amount", row_r.SalesAmount + row_r.TaxAmt);
        }

    }
    }
    yield return output.AsReadOnly();
}
}
```

<span data-ttu-id="99449-480">W tym scenariuszu przypadek użycia możemy są budowania raportu analizy sprzedaży detalicznej.</span><span class="sxs-lookup"><span data-stu-id="99449-480">In this use-case scenario, we are building an analytics report for the retailer.</span></span> <span data-ttu-id="99449-481">Celem jest, aby znaleźć wszystkie produkty, które koszt ponad 20 000 $ i który sprzedaży za pośrednictwem witryny sieci Web szybciej niż w sprzedaży detalicznej regularnie w danym okresie.</span><span class="sxs-lookup"><span data-stu-id="99449-481">The goal is to find all products that cost more than $20,000 and that sell through the website faster than through the regular retailer within a certain time frame.</span></span>

<span data-ttu-id="99449-482">Poniżej przedstawiono podstawowe skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="99449-482">Here is the base U-SQL script.</span></span> <span data-ttu-id="99449-483">Możesz porównać logiki między sprzężenia regularnego i łączenia:</span><span class="sxs-lookup"><span data-stu-id="99449-483">You can compare the logic between a regular JOIN and a combiner:</span></span>

```sql
DECLARE @LocalURI string = @"\usql-programmability\";

DECLARE @input_file_internet_sales string = @LocalURI+"FactInternetSales.txt";
DECLARE @input_file_reseller_sales string = @LocalURI+"FactResellerSales.txt";
DECLARE @output_file1 string = @LocalURI+"output_file1.tsv";
DECLARE @output_file2 string = @LocalURI+"output_file2.tsv";

@fact_internet_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    CustomerKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_internet_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@fact_reseller_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    ResellerKey int ,
    EmployeeKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_reseller_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@rs1 =
SELECT
    fis.OrderDateKey,
    fis.ProductKey,
    fis.SalesAmount+fis.TaxAmt AS Internet_Sales_Amount,
    frs.SalesAmount+frs.TaxAmt AS Reseller_Sales_Amount
FROM @fact_internet_sales AS fis
     INNER JOIN @fact_reseller_sales AS frs
     ON fis.ProductKey == frs.ProductKey
WHERE
    fis.OrderDateKey < frs.OrderDateKey
    AND fis.OrderDateKey == 20010701
    AND frs.SalesAmount+frs.TaxAmt > 20000;

@rs2 =
COMBINE @fact_internet_sales AS fis
WITH @fact_reseller_sales AS frs
ON fis.ProductKey == frs.ProductKey
PRODUCE OrderDateKey int,
        ProductKey int,
        Internet_Sales_Amount decimal,
        Reseller_Sales_Amount decimal
USING new USQL_Programmability.CombineSales();

OUTPUT @rs1 TO @output_file1 USING Outputters.Tsv();
OUTPUT @rs2 TO @output_file2 USING Outputters.Tsv();
```

<span data-ttu-id="99449-484">Zdefiniowane przez użytkownika łączenia można wywołać jako nowe wystąpienie obiektu applier:</span><span class="sxs-lookup"><span data-stu-id="99449-484">A user-defined combiner can be called as a new instance of the applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="99449-485">Lub wywołanie metody fabryki otoki:</span><span class="sxs-lookup"><span data-stu-id="99449-485">Or with the invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="99449-486">Użyj reduktory zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="99449-486">Use user-defined reducers</span></span>

<span data-ttu-id="99449-487">U-SQL umożliwia pisanie reduktory niestandardowego zestawu wierszy w języku C# z wykorzystaniem strukturę rozszerzalności zdefiniowane przez użytkownika operatora i implementowanie interfejsu IReducer.</span><span class="sxs-lookup"><span data-stu-id="99449-487">U-SQL enables you to write custom rowset reducers in C# by using the user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="99449-488">Reduktor zdefiniowane przez użytkownika lub przez, można usunąć niepotrzebne wierszy podczas wyodrębniania danych (Importuj).</span><span class="sxs-lookup"><span data-stu-id="99449-488">User-defined reducer, or UDR, can be used to eliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="99449-489">On również można manipulować i ocena wierszy i kolumn.</span><span class="sxs-lookup"><span data-stu-id="99449-489">It also can be used to manipulate and evaluate rows and columns.</span></span> <span data-ttu-id="99449-490">Opartych na logice programowania, jego można również zdefiniować wiersze, które muszą zostać wyodrębniony.</span><span class="sxs-lookup"><span data-stu-id="99449-490">Based on programmability logic, it can also define which rows need to be extracted.</span></span>

<span data-ttu-id="99449-491">Aby zdefiniować przez klasę, należy utworzyć `IReducer` interfejsu z opcjonalną `SqlUserDefinedReducer` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="99449-491">To define a UDR class, we need to create an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="99449-492">Ten interfejs klasy powinny zawierać definicji `IEnumerable` zastąpienie interfejsu zestawu wierszy.</span><span class="sxs-lookup"><span data-stu-id="99449-492">This class interface should contain a definition for the `IEnumerable` interface rowset override.</span></span>

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
        …
    }

}
```

<span data-ttu-id="99449-493">**SqlUserDefinedReducer** atrybut wskazuje, że typ powinien być zarejestrowany jako reduktor zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-493">The **SqlUserDefinedReducer** attribute indicates that the type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="99449-494">Ta klasa nie może być dziedziczona.</span><span class="sxs-lookup"><span data-stu-id="99449-494">This class cannot be inherited.</span></span>
<span data-ttu-id="99449-495">**SqlUserDefinedReducer** jest opcjonalny atrybut dla definicji reduktor zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="99449-496">Służy do definiowania właściwości IsRecursive.</span><span class="sxs-lookup"><span data-stu-id="99449-496">It's used to define IsRecursive property.</span></span>

* <span data-ttu-id="99449-497">wartość logiczna IsRecursive</span><span class="sxs-lookup"><span data-stu-id="99449-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="99449-498">**wartość true,** = wskazuje, czy ta reduktor jest idempotentności</span><span class="sxs-lookup"><span data-stu-id="99449-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="99449-499">Obiekty główne programowania są **wejściowych** i **dane wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="99449-499">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="99449-500">Obiekt wejściowy jest używany do wyliczenia wiersze danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="99449-500">The input object is used to enumerate input rows.</span></span> <span data-ttu-id="99449-501">Dane wyjściowe służy do ustawiania wiersze danych wyjściowych wyniku zmniejszenie działania.</span><span class="sxs-lookup"><span data-stu-id="99449-501">Output is used to set output rows as a result of reducing activity.</span></span>

<span data-ttu-id="99449-502">Wyliczenia wiersze danych wejściowych używamy `Row.Get` metody.</span><span class="sxs-lookup"><span data-stu-id="99449-502">For input rows enumeration, we use the `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="99449-503">Parametr `Row.Get` metody jest przekazywany jako część kolumny `PRODUCE` klasy `REDUCE` instrukcji podstawowy skrypt U-SQL.</span><span class="sxs-lookup"><span data-stu-id="99449-503">The parameter for the `Row.Get` method is a column that's passed as part of the `PRODUCE` class of the `REDUCE` statement of the U-SQL base script.</span></span> <span data-ttu-id="99449-504">Należy również za pomocą prawidłowy typ danych w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="99449-504">We need to use the correct data type here as well.</span></span>

<span data-ttu-id="99449-505">Dla danych wyjściowych, użyj `output.Set` metody.</span><span class="sxs-lookup"><span data-stu-id="99449-505">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="99449-506">Ważne jest, aby zrozumieć, w tym niestandardowych reduktor tylko wartości, które są zdefiniowane z danych wyjściowych `output.Set` wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="99449-506">It is important to understand that custom reducer only outputs values that are defined with the `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="99449-507">Dane wyjściowe rzeczywiste reduktor zostanie wywołany przez wywołanie metody `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="99449-507">The actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="99449-508">Poniżej przedstawiono przykład reduktor:</span><span class="sxs-lookup"><span data-stu-id="99449-508">Following is a reducer example:</span></span>

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
    string guid;
    DateTime dt;
    string user;
    string des;

    foreach (IRow row in input.Rows)
    {
        guid = row.Get<string>("guid");
        dt = row.Get<DateTime>("dt");
        user = row.Get<string>("user");
        des = row.Get<string>("des");

        if (user.Length > 0)
        {
        output.Set<string>("guid", guid);
        output.Set<DateTime>("dt", dt);
        output.Set<string>("user", user);
        output.Set<string>("des", des);

        yield return output.AsReadOnly();
        }
    }
    }

}
```

<span data-ttu-id="99449-509">W tym scenariuszu przypadek użycia reduktor pomija wiersze z Pusta nazwa użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-509">In this use-case scenario, the reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="99449-510">Dla każdego wiersza w zestawie wierszy go odczytuje każdej wymaganej kolumny, a następnie oblicza długość nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99449-510">For each row in rowset, it reads each required column, then evaluates the length of the user name.</span></span> <span data-ttu-id="99449-511">Rzeczywiste wiersza go generuje tylko wtedy, gdy długość wartości nazwy użytkownika jest większa niż 0.</span><span class="sxs-lookup"><span data-stu-id="99449-511">It outputs the actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="99449-512">Poniżej przedstawiono podstawowy skryptu U-SQL, który używa niestandardowych reduktor:</span><span class="sxs-lookup"><span data-stu-id="99449-512">Following is base U-SQL script that uses a custom reducer:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file_reducer.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    REDUCE @rs0 PRESORT guid
    ON guid  
    PRODUCE guid string, dt DateTime, user String, des String
    USING new USQL_Programmability.EmptyUserReducer();

@rs2 =
    SELECT guid AS start_id,
           dt AS start_time,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS start_fiscalperiod,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    TO @output_file 
    USING Outputters.Text();
```
