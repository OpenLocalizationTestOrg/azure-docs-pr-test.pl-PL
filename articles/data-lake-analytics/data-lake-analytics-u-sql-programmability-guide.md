---
title: "Podręcznik programowania aaaU SQL dla usługi Azure Data Lake | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello zbiór usług w usłudze Azure Data Lake umożliwiających toocreate platformy danych big data oparte na chmurze."
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
ms.openlocfilehash: cc8f126234c6106a0dc633ce85a1d9ab1e634e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="c5de2-103">Podręcznik programowania U-SQL</span><span class="sxs-lookup"><span data-stu-id="c5de2-103">U-SQL programmability guide</span></span>

<span data-ttu-id="c5de2-104">U-SQL jest język zapytania, które jest przeznaczone do typów danych dużych obciążeń.</span><span class="sxs-lookup"><span data-stu-id="c5de2-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="c5de2-105">Jednym z hello funkcji U-SQL jest hello kombinację hello deklaratywne języka przypominającego SQL o rozszerzalności hello i programowania, który znajduje się w języku C#.</span><span class="sxs-lookup"><span data-stu-id="c5de2-105">One of hello unique features of U-SQL is hello combination of hello SQL-like declarative language with hello extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="c5de2-106">W tym przewodniku możemy skupić się na powitania rozszerzania i programowania hello języka U-SQL, który został włączony w języku C#.</span><span class="sxs-lookup"><span data-stu-id="c5de2-106">In this guide, we concentrate on hello extensibility and programmability of hello U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="c5de2-107">Wymagania</span><span class="sxs-lookup"><span data-stu-id="c5de2-107">Requirements</span></span>

<span data-ttu-id="c5de2-108">Pobierz i zainstaluj [Azure Data Lake Tools dla programu Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="c5de2-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="c5de2-109">Wprowadzenie do języka U-SQL</span><span class="sxs-lookup"><span data-stu-id="c5de2-109">Get started with U-SQL</span></span>  

<span data-ttu-id="c5de2-110">Przyjrzyjmy się hello następującego skryptu U-SQL:</span><span class="sxs-lookup"><span data-stu-id="c5de2-110">Let’s look at hello following U-SQL script:</span></span>

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

<span data-ttu-id="c5de2-111">Definiuje zestawu wierszy o nazwie @a i tworzy zestawu wierszy o nazwie @results z @a.</span><span class="sxs-lookup"><span data-stu-id="c5de2-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="c5de2-112">Typy C# i wyrażenia w skryptu U-SQL</span><span class="sxs-lookup"><span data-stu-id="c5de2-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="c5de2-113">Wyrażenie U-SQL jest wyrażenie C# połączone z operacji logicznych U-SQL takich `AND`, `OR`, i `NOT`.</span><span class="sxs-lookup"><span data-stu-id="c5de2-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="c5de2-114">Wyrażenia języka U-SQL mogą być używane z SELECT, EXTRACT, gdzie wystąpienia, Grupuj według, ZADEKLAROWAĆ.</span><span class="sxs-lookup"><span data-stu-id="c5de2-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="c5de2-115">Na przykład hello następującego skryptu analizuje ciąg, wartość daty i godziny w klauzuli SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="c5de2-115">For example, hello following script parses a string a DateTime value in hello SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="c5de2-116">Witaj poniższy skrypt analizuje ciąg wartość daty i godziny w instrukcji DECLARE.</span><span class="sxs-lookup"><span data-stu-id="c5de2-116">hello following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="c5de2-117">Używanie wyrażeń C# dla konwersje typów danych</span><span class="sxs-lookup"><span data-stu-id="c5de2-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="c5de2-118">Witaj poniższy przykład pokazuje, jak data/godzina konwersji danych za pomocą wyrażeń C#.</span><span class="sxs-lookup"><span data-stu-id="c5de2-118">hello following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="c5de2-119">W tym scenariuszu określonego danych dotyczących ciągu daty/godziny to data i godzina przekonwertowanego toostandard o północy 00:00:00 czasu notacji.</span><span class="sxs-lookup"><span data-stu-id="c5de2-119">In this particular scenario, string datetime data is converted toostandard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="c5de2-120">Używanie wyrażeń C# dla bieżącej daty</span><span class="sxs-lookup"><span data-stu-id="c5de2-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="c5de2-121">toopull dzisiaj, możemy użyć powitania po wyrażeniu C#:</span><span class="sxs-lookup"><span data-stu-id="c5de2-121">toopull today’s date, we can use hello following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="c5de2-122">Poniżej przedstawiono przykładowy sposób toouse tego wyrażenia w skrypcie:</span><span class="sxs-lookup"><span data-stu-id="c5de2-122">Here's an example of how toouse this expression in a script:</span></span>

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



## <a name="using-net-assemblies"></a><span data-ttu-id="c5de2-123">Za pomocą zestawów platformy .NET</span><span class="sxs-lookup"><span data-stu-id="c5de2-123">Using .NET assemblies</span></span>
<span data-ttu-id="c5de2-124">U-SQL modelu rozszerzalności odgrywa hello możliwości tooadd niestandardowego kodu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-124">U-SQL’s extensibility model relies heavily on hello ability tooadd custom code.</span></span> <span data-ttu-id="c5de2-125">Obecnie U-SQL zapewnia łatwy sposób tooadd własnych firmy Microsoft. Kod na podstawie sieci (w szczególności, C#).</span><span class="sxs-lookup"><span data-stu-id="c5de2-125">Currently, U-SQL provides you with easy ways tooadd your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="c5de2-126">Jednak można również dodać kodu niestandardowego, który jest zapisywany w innych językach .NET, takie jak VB.NET lub F #.</span><span class="sxs-lookup"><span data-stu-id="c5de2-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="c5de2-127">Rejestrowanie zestawów platformy .NET</span><span class="sxs-lookup"><span data-stu-id="c5de2-127">Register a .NET assembly</span></span>

<span data-ttu-id="c5de2-128">Użyj hello utworzyć zestaw instrukcji tooplace zestaw .NET do języka U-SQL bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c5de2-128">Use hello CREATE ASSEMBLY statement tooplace a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="c5de2-129">Po zestaw znajduje się w bazie danych, w skryptów U-SQL przy użyciu instrukcji zestaw odwołania hello można użyć tych zestawów.</span><span class="sxs-lookup"><span data-stu-id="c5de2-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using hello REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="c5de2-130">Witaj następującego kodu pokazuje sposób tooregister zestawu:</span><span class="sxs-lookup"><span data-stu-id="c5de2-130">hello following code shows how tooregister an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="c5de2-131">Witaj następującego kodu pokazuje sposób tooreference zestawu:</span><span class="sxs-lookup"><span data-stu-id="c5de2-131">hello following code shows how tooreference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="c5de2-132">Zapoznaj się hello [instrukcje rejestracji zestawu](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) który obejmuje w tym temacie bardziej szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="c5de2-132">Consult hello [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="c5de2-133">Użyj wersji zestawu</span><span class="sxs-lookup"><span data-stu-id="c5de2-133">Use assembly versioning</span></span>
<span data-ttu-id="c5de2-134">Obecnie U-SQL używa hello .NET Framework w wersji 4.5.</span><span class="sxs-lookup"><span data-stu-id="c5de2-134">Currently, U-SQL uses hello .NET Framework version 4.5.</span></span> <span data-ttu-id="c5de2-135">Dlatego upewnij się, że własne zestawy są zgodne z tą wersją środowiska uruchomieniowego hello.</span><span class="sxs-lookup"><span data-stu-id="c5de2-135">So ensure that your own assemblies are compatible with that version of hello runtime.</span></span>

<span data-ttu-id="c5de2-136">Jak wspomniano wcześniej, kod działa U-SQL w formacie 64-bitowej (x 64).</span><span class="sxs-lookup"><span data-stu-id="c5de2-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="c5de2-137">Dlatego upewnij się, że kod jest skompilowany toorun na x64.</span><span class="sxs-lookup"><span data-stu-id="c5de2-137">So make sure that your code is compiled toorun on x64.</span></span> <span data-ttu-id="c5de2-138">W przeciwnym razie błąd hello niepoprawny format przedstawiona wcześniej.</span><span class="sxs-lookup"><span data-stu-id="c5de2-138">Otherwise you get hello incorrect format error shown earlier.</span></span>

<span data-ttu-id="c5de2-139">Każdy przekazany zestaw biblioteki DLL i pliku zasobów, takich jak innego środowiska uruchomieniowego, natywny zestaw lub pliku konfiguracji, może mieć maksymalnie 400 MB.</span><span class="sxs-lookup"><span data-stu-id="c5de2-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="c5de2-140">Całkowity rozmiar Hello wdrożonych zasobów za pomocą wdrażania zasobów lub za pośrednictwem tooassemblies odwołań i dodatkowe pliki, nie może przekraczać 3 GB.</span><span class="sxs-lookup"><span data-stu-id="c5de2-140">hello total size of deployed resources, either via DEPLOY RESOURCE or via references tooassemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="c5de2-141">Na koniec należy pamiętać, że każda baza danych U-SQL może zawierać tylko jedną wersję żadnych danego zestawu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="c5de2-142">Na przykład, jeśli potrzebujesz zarówno w wersji 7, jak i w wersji 8 hello biblioteki NewtonSoft Json.Net, należy tooregister w dwóch różnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="c5de2-142">For example, if you need both version 7 and version 8 of hello NewtonSoft Json.Net library, you need tooregister them in two different databases.</span></span> <span data-ttu-id="c5de2-143">Ponadto każdy skrypt może odwoływać się tylko wersję tooone danego zestawu biblioteki DLL.</span><span class="sxs-lookup"><span data-stu-id="c5de2-143">Furthermore, each script can only refer tooone version of a given assembly DLL.</span></span> <span data-ttu-id="c5de2-144">W związku z tym U-SQL następuje hello C# zestawu zarządzania i wersji semantyki.</span><span class="sxs-lookup"><span data-stu-id="c5de2-144">In this respect, U-SQL follows hello C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="c5de2-145">Użyj funkcji zdefiniowanej przez użytkownika: funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="c5de2-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="c5de2-146">Funkcje zdefiniowane przez użytkownika U-SQL lub funkcji zdefiniowanej przez użytkownika, są programowania procedur, które akceptują parametrów, wykonywania akcji (na przykład złożonych obliczeń) i zwraca wynik hello tego działania jako wartość.</span><span class="sxs-lookup"><span data-stu-id="c5de2-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return hello result of that action as a value.</span></span> <span data-ttu-id="c5de2-147">Witaj zwracać wartość funkcji zdefiniowanej przez użytkownika może być tylko jeden skalarnej.</span><span class="sxs-lookup"><span data-stu-id="c5de2-147">hello return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="c5de2-148">UDF języka U-SQL może zostać wywołany w podstawowej skryptu U-SQL, takich jak wszystkie inne C# skalarną.</span><span class="sxs-lookup"><span data-stu-id="c5de2-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="c5de2-149">Firma Microsoft zaleca, aby zainicjować U-SQL funkcje zdefiniowane przez użytkownika jako **publicznego** i **statycznych**.</span><span class="sxs-lookup"><span data-stu-id="c5de2-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="c5de2-150">Pierwszy Przyjrzyjmy się hello prosty przykład tworzenia funkcji zdefiniowanej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5de2-150">First let’s look at hello simple example of creating a UDF.</span></span>

<span data-ttu-id="c5de2-151">W tym scenariuszu przypadek użycia potrzebujemy toodetermine hello okres, w tym hello kwartał i miesiąc obrachunkowy hello pierwszego logowania dla określonego użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="c5de2-151">In this use-case scenario, we need toodetermine hello fiscal period, including hello fiscal quarter and fiscal month of hello first sign-in for hello specific user.</span></span> <span data-ttu-id="c5de2-152">Witaj pierwszy miesiąc obrachunkowy roku hello w naszym scenariuszu jest czerwca.</span><span class="sxs-lookup"><span data-stu-id="c5de2-152">hello first fiscal month of hello year in our scenario is June.</span></span>

<span data-ttu-id="c5de2-153">okres toocalculate wprowadzeniu powitania po funkcji języka C#:</span><span class="sxs-lookup"><span data-stu-id="c5de2-153">toocalculate fiscal period, we introduce hello following C# function:</span></span>

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

<span data-ttu-id="c5de2-154">Po prostu oblicza miesiąc obrachunkowy i kwartał i zwraca wartość typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="c5de2-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="c5de2-155">Czerwca, hello pierwszy miesiąc hello pierwszy kwartał używamy "Q1:P1".</span><span class="sxs-lookup"><span data-stu-id="c5de2-155">For June, hello first month of hello first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="c5de2-156">Lipca możemy użyć "Q1:P2" i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="c5de2-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="c5de2-157">To normalne działanie C# pracujemy toouse będzie w naszym projektu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c5de2-157">This is a regular C# function that we are going toouse in our U-SQL project.</span></span>

<span data-ttu-id="c5de2-158">Poniżej przedstawiono wygląd hello związane z kodem sekcji w tym scenariuszu:</span><span class="sxs-lookup"><span data-stu-id="c5de2-158">Here is how hello code-behind section looks in this scenario:</span></span>

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

<span data-ttu-id="c5de2-159">Teraz zamierzamy toocall tej funkcji z hello podstawowy skrypt U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c5de2-159">Now we are going toocall this function from hello base U-SQL script.</span></span> <span data-ttu-id="c5de2-160">toodo, mamy tooprovide w pełni kwalifikowanej nazwy funkcji hello, włącznie z przestrzenią nazw hello, czyli w tym przypadku NameSpace.Class.Function(parameter).</span><span class="sxs-lookup"><span data-stu-id="c5de2-160">toodo this, we have tooprovide a fully qualified name for hello function, including hello namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="c5de2-161">Rzeczywiste skrypt bazowy hello U-SQL jest następujący:</span><span class="sxs-lookup"><span data-stu-id="c5de2-161">Following is hello actual U-SQL base script:</span></span>

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
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="c5de2-162">Plik wyjściowy hello wykonywania skryptów hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="c5de2-162">Following is hello output file of hello script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="c5de2-163">W tym przykładzie przedstawiono prosty użycie wbudowanej funkcji zdefiniowanej przez użytkownika w języku U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c5de2-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="c5de2-164">Zachowaj stanu między wywołań funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="c5de2-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="c5de2-165">Obiekty programowania U-SQL C# można można bardziej zaawansowane opcje, wykorzystując interakcyjności za pomocą zmiennych globalnych hello związane z kodem.</span><span class="sxs-lookup"><span data-stu-id="c5de2-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through hello code-behind global variables.</span></span> <span data-ttu-id="c5de2-166">Przyjrzyjmy się powitania po scenariusza biznesowego przypadek użycia.</span><span class="sxs-lookup"><span data-stu-id="c5de2-166">Let’s look at hello following business use-case scenario.</span></span>

<span data-ttu-id="c5de2-167">W dużych organizacjach użytkownicy mogą przełączać odmian wewnętrznych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c5de2-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="c5de2-168">Obejmują one programu Microsoft Dynamics CRM, usługa Power Bi i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="c5de2-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="c5de2-169">Klienci mogą też chcieć tooapply analizy telemetrii sposób użytkownicy będą przełączać się między różnymi aplikacjami, jakie użycia hello trendy są i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="c5de2-169">Customers might want tooapply a telemetry analysis of how users switch between different applications, what hello usage trends are, and so on.</span></span> <span data-ttu-id="c5de2-170">Celem Hello dla firm hello jest toooptimize użycia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c5de2-170">hello goal for hello business is toooptimize application usage.</span></span> <span data-ttu-id="c5de2-171">Są też toocombine różnych aplikacji lub określonych procedur logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="c5de2-171">They also might want toocombine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="c5de2-172">tooachieve tego celu, będziemy mieć identyfikatory sesji toodetermine i czas opóźnienia między hello ostatniej sesji, który wystąpił.</span><span class="sxs-lookup"><span data-stu-id="c5de2-172">tooachieve this goal, we have toodetermine session IDs and lag time between hello last session that occurred.</span></span>

<span data-ttu-id="c5de2-173">Firma Microsoft muszą toofind poprzedniego logowanie, a następnie przypisz tej sesji logowania tooall, które są generowane toohello tej samej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c5de2-173">We need toofind a previous sign-in and then assign this sign-in tooall sessions that are being generated toohello same application.</span></span> <span data-ttu-id="c5de2-174">pierwszego wyzwania Hello jest, że podstawowy skrypt U-SQL nie zezwala na nam obliczeń tooapply za pośrednictwem już obliczane kolumny z funkcja LAG.</span><span class="sxs-lookup"><span data-stu-id="c5de2-174">hello first challenge is that U-SQL base script doesn't allow us tooapply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="c5de2-175">Witaj drugi wyzwaniem jest czy mamy tookeep hello określonej sesji dla wszystkich sesji w ramach hello sam okres czasu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-175">hello second challenge is that we have tookeep hello specific session for all sessions within hello same time period.</span></span>

<span data-ttu-id="c5de2-176">toosolve ten problem, używamy zmiennej globalnej wewnątrz sekcji CodeBehind: `static public string globalSession;`.</span><span class="sxs-lookup"><span data-stu-id="c5de2-176">toosolve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="c5de2-177">Tę zmienną globalną jest stosowane toohello całego zestawu wierszy podczas wykonywania naszych skryptu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-177">This global variable is applied toohello entire rowset during our script execution.</span></span>

<span data-ttu-id="c5de2-178">Oto hello związane z kodem sekcji nasz program U-SQL:</span><span class="sxs-lookup"><span data-stu-id="c5de2-178">Here is hello code-behind section of our U-SQL program:</span></span>

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

<span data-ttu-id="c5de2-179">W tym przykładzie przedstawiono hello zmiennej globalnej `static public string globalSession;` używany wewnątrz hello `getStampUserSession` funkcji i uzyskiwanie za każdego hello czasu sesji parametr zostanie zmieniona.</span><span class="sxs-lookup"><span data-stu-id="c5de2-179">This example shows hello global variable `static public string globalSession;` used inside hello `getStampUserSession` function and getting reinitialized each time hello Session parameter is changed.</span></span>

<span data-ttu-id="c5de2-180">Witaj podstawowy skrypt U-SQL jest następujący:</span><span class="sxs-lookup"><span data-stu-id="c5de2-180">hello U-SQL base script is as follows:</span></span>

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
    too@out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

<span data-ttu-id="c5de2-181">Funkcja `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` jest tutaj wywoływana podczas obliczania wierszy pamięci drugi hello.</span><span class="sxs-lookup"><span data-stu-id="c5de2-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during hello second memory rowset calculation.</span></span> <span data-ttu-id="c5de2-182">Przekazuje ono hello `UserSessionTimestamp` kolumny i zwraca wartość, dopóki hello `UserSessionTimestamp` została zmieniona.</span><span class="sxs-lookup"><span data-stu-id="c5de2-182">It passes hello `UserSessionTimestamp` column and returns hello value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="c5de2-183">Plik wyjściowy Hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="c5de2-183">hello output file is as follows:</span></span>

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

<span data-ttu-id="c5de2-184">W tym przykładzie przedstawiono bardziej skomplikowane scenariusz przypadek użycia, w której używamy zmiennej globalnej wewnątrz sekcji związane z kodem, która jest stosowane toohello całej pamięci wierszy.</span><span class="sxs-lookup"><span data-stu-id="c5de2-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied toohello entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="c5de2-185">Używanie typów zdefiniowanych przez użytkownika: UDT</span><span class="sxs-lookup"><span data-stu-id="c5de2-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="c5de2-186">Typy definiowane przez użytkownika lub UDT, jest inna funkcja programowalności U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c5de2-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="c5de2-187">UDT U-SQL zachowuje się jak zwykły C# zdefiniowane przez użytkownika typu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="c5de2-188">C# to silnie typizowaną język, który umożliwia wykorzystanie hello wbudowane i niestandardowe typy danych zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5de2-188">C# is a strongly typed language that allows hello use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="c5de2-189">U-SQL nie można niejawnie serializacji lub zdeserializować dowolnego UDTs podczas przekazywania hello UDT między wierzchołków w zestawów wierszy.</span><span class="sxs-lookup"><span data-stu-id="c5de2-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when hello UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="c5de2-190">Oznacza to, że hello, które użytkownik ma tooprovide jawne elementu formatującego za pomocą interfejsu IFormatter hello.</span><span class="sxs-lookup"><span data-stu-id="c5de2-190">This means that hello user has tooprovide an explicit formatter by using hello IFormatter interface.</span></span> <span data-ttu-id="c5de2-191">Zapewnia to U-SQL z hello serializacji i deserializacji metody hello UDT.</span><span class="sxs-lookup"><span data-stu-id="c5de2-191">This provides U-SQL with hello serialize and de-serialize methods for hello UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="c5de2-192">U-SQL ekstraktory wbudowanych i outputters obecnie nie można serializować lub zdeserializować UDT tooor danych z plików, nawet w przypadku hello IFormatter zestawu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data tooor from files even with hello IFormatter set.</span></span> <span data-ttu-id="c5de2-193">Dlatego podczas pisania pliku tooa danych UDT hello danych wyjściowych instrukcji lub odczytywania go z katalogu, możesz mieć toopass go w formie ciągu lub tablicy typu byte.</span><span class="sxs-lookup"><span data-stu-id="c5de2-193">So when you're writing UDT data tooa file with hello OUTPUT statement, or reading it with an extractor, you have toopass it as a string or byte array.</span></span> <span data-ttu-id="c5de2-194">Następnie wywołaj hello serializacji i deserializacji kodu (to znaczy metodę ToString() hello UDT) jawnie.</span><span class="sxs-lookup"><span data-stu-id="c5de2-194">Then you call hello serialization and deserialization code (that is, hello UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="c5de2-195">Zdefiniowane przez użytkownika ekstraktory outputters na powitania innych ręcznie, może Odczyt i zapis typów.</span><span class="sxs-lookup"><span data-stu-id="c5de2-195">User-defined extractors and outputters, on hello other hand, can read and write UDTs.</span></span>

<span data-ttu-id="c5de2-196">Jeśli chcesz ponowić toouse UDT w katalogu lub OUTPUTTER (Brak poprzedniej wybierz), jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="c5de2-196">If we try toouse UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="c5de2-197">Otrzymaliśmy hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="c5de2-197">We receive hello following error:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used toooutput column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how tooserialize this type, or call a serialization method on hello type in
hello preceding SELECT. C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

<span data-ttu-id="c5de2-198">toowork z UDT w outputter albo mamy tooserialize on toostring z hello metodę ToString() lub Utwórz niestandardowe outputter.</span><span class="sxs-lookup"><span data-stu-id="c5de2-198">toowork with UDT in outputter, we either have tooserialize it toostring with hello ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="c5de2-199">Typów nie można obecnie używać w GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="c5de2-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="c5de2-200">Jeśli UDT jest używany w GROUP BY, jest zgłaszany hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="c5de2-200">If UDT is used in GROUP BY, hello following error is thrown:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want toouse with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

<span data-ttu-id="c5de2-201">toodefine UDT, konieczne jest:</span><span class="sxs-lookup"><span data-stu-id="c5de2-201">toodefine a UDT, we have to:</span></span>

* <span data-ttu-id="c5de2-202">Dodaj następujące obszary nazw hello:</span><span class="sxs-lookup"><span data-stu-id="c5de2-202">Add hello following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="c5de2-203">Dodaj `Microsoft.Analytics.Interfaces`, co jest wymagane dla interfejsów UDT hello.</span><span class="sxs-lookup"><span data-stu-id="c5de2-203">Add `Microsoft.Analytics.Interfaces`, which is required for hello UDT interfaces.</span></span> <span data-ttu-id="c5de2-204">Ponadto `System.IO` może być wymagane toodefine hello IFormatter interfejsu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-204">In addition, `System.IO` might be needed toodefine hello IFormatter interface.</span></span>

* <span data-ttu-id="c5de2-205">Zdefiniuj typ zdefiniowane z atrybutem SqlUserDefinedType.</span><span class="sxs-lookup"><span data-stu-id="c5de2-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="c5de2-206">**SqlUserDefinedType** jest definicją typu w zestawie co typ zdefiniowany przez użytkownika (UDT) toomark używanych w języku U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c5de2-206">**SqlUserDefinedType** is used toomark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="c5de2-207">właściwości Hello atrybutu hello odzwierciedlają hello charakterystyki fizycznej hello UDT.</span><span class="sxs-lookup"><span data-stu-id="c5de2-207">hello properties on hello attribute reflect hello physical characteristics of hello UDT.</span></span> <span data-ttu-id="c5de2-208">Ta klasa nie może być dziedziczona.</span><span class="sxs-lookup"><span data-stu-id="c5de2-208">This class cannot be inherited.</span></span>

<span data-ttu-id="c5de2-209">SqlUserDefinedType jest wymagany atrybut UDT definicji.</span><span class="sxs-lookup"><span data-stu-id="c5de2-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="c5de2-210">Witaj konstruktora klasy hello:</span><span class="sxs-lookup"><span data-stu-id="c5de2-210">hello constructor of hello class:</span></span>  

* <span data-ttu-id="c5de2-211">SqlUserDefinedTypeAttribute (elementu formatującego typu)</span><span class="sxs-lookup"><span data-stu-id="c5de2-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="c5de2-212">Program formatujący typ: wymagany parametr toodefine program formatujący UDT — w szczególności hello typu hello `IFormatter` interfejsu muszą być przekazywane w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-212">Type formatter: Required parameter toodefine an UDT formatter--specifically, hello type of hello `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="c5de2-213">Typowy UDT wymaga również definicji interfejsu IFormatter hello, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="c5de2-213">Typical UDT also requires definition of hello IFormatter interface, as shown in hello following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="c5de2-214">Witaj `IFormatter` interfejsu serializuje i zwalnia serializuje wykres obiektu typu głównego hello \<typeparamref name = "T" >.</span><span class="sxs-lookup"><span data-stu-id="c5de2-214">hello `IFormatter` interface serializes and de-serializes an object graph with hello root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="c5de2-215">\<typeparam name = "T" > Witaj typu głównego dla tooserialize wykresu obiektu hello i zdeserializować.</span><span class="sxs-lookup"><span data-stu-id="c5de2-215">\<typeparam name="T">hello root type for hello object graph tooserialize and de-serialize.</span></span>

* <span data-ttu-id="c5de2-216">**Deserializacja**: cofnąć serializuje dane hello w strumieniu hello podane i reconstitutes hello wykresu obiektów.</span><span class="sxs-lookup"><span data-stu-id="c5de2-216">**Deserialize**: De-serializes hello data on hello provided stream and reconstitutes hello graph of objects.</span></span>

* <span data-ttu-id="c5de2-217">**Serializować**: Serializuje obiekt lub grafu obiektów, z hello danego strumienia toohello podane głównego.</span><span class="sxs-lookup"><span data-stu-id="c5de2-217">**Serialize**: Serializes an object, or graph of objects, with hello given root toohello provided stream.</span></span>

<span data-ttu-id="c5de2-218">`MyType`wystąpienie: wystąpienie typu hello.</span><span class="sxs-lookup"><span data-stu-id="c5de2-218">`MyType` instance: Instance of hello type.</span></span>  
<span data-ttu-id="c5de2-219">`IColumnWriter`Moduł zapisujący / `IColumnReader` czytnika: hello bazowy strumieniu kolumny.</span><span class="sxs-lookup"><span data-stu-id="c5de2-219">`IColumnWriter` writer / `IColumnReader` reader: hello underlying column stream.</span></span>  
<span data-ttu-id="c5de2-220">`ISerializationContext`kontekst: wyliczenia, który definiuje zestaw flagi określa hello źródłowy lub docelowy kontekst dla strumienia hello podczas serializacji.</span><span class="sxs-lookup"><span data-stu-id="c5de2-220">`ISerializationContext` context: Enum that defines a set of flags that specifies hello source or destination context for hello stream during serialization.</span></span>

* <span data-ttu-id="c5de2-221">**Pośredni**: Określa kontekst tego hello źródłowy lub docelowy nie jest utrwalonego magazynu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-221">**Intermediate**: Specifies that hello source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="c5de2-222">**Trwałość**: Określa kontekst tego hello źródłowy lub docelowy jest utrwalonego magazynu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-222">**Persistence**: Specifies that hello source or destination context is a persisted store.</span></span>

<span data-ttu-id="c5de2-223">Jako regularne C# typ, definicji UDT U-SQL mogą zawierać zastąpień dla operatorów takich jak +/ == /! =.</span><span class="sxs-lookup"><span data-stu-id="c5de2-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="c5de2-224">Może również obejmować metod statycznych.</span><span class="sxs-lookup"><span data-stu-id="c5de2-224">It can also include static methods.</span></span> <span data-ttu-id="c5de2-225">Na przykład, jeśli zamierzamy toouse tego UDT jako tooa parametru funkcji agregującej MIN U-SQL, mamy toodefine < zastąpienie operatora.</span><span class="sxs-lookup"><span data-stu-id="c5de2-225">For example, if we are going toouse this UDT as a parameter tooa U-SQL MIN aggregate function, we have toodefine < operator override.</span></span>

<span data-ttu-id="c5de2-226">Wcześniej w tym przewodniku firma Microsoft przedstawiono przykład obrachunkowym identyfikacji okresu od określonej daty hello w formacie hello Qn:Pn (Q1:P10).</span><span class="sxs-lookup"><span data-stu-id="c5de2-226">Earlier in this guide, we demonstrated an example for fiscal period identification from hello specific date in hello format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="c5de2-227">Witaj poniższy przykład pokazuje, jak toodefine niestandardowego typu wartości okresu obrachunkowym.</span><span class="sxs-lookup"><span data-stu-id="c5de2-227">hello following example shows how toodefine a custom type for fiscal period values.</span></span>

<span data-ttu-id="c5de2-228">Poniżej przedstawiono przykład sekcji kodu powiązanego z niestandardowy interfejs UDT i IFormatter:</span><span class="sxs-lookup"><span data-stu-id="c5de2-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

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

<span data-ttu-id="c5de2-229">Witaj zdefiniowanego typu zawiera dwie liczb: kwartał i miesiąc.</span><span class="sxs-lookup"><span data-stu-id="c5de2-229">hello defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="c5de2-230">Operatory == /! = / > / < a statyczną metodę ToString() są zdefiniowane w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="c5de2-231">Jak wspomniano wcześniej, można używać w wyrażeniach wybierz UDT, ale nie można używać w OUTPUTTER/EKSTRAKTOR bez niestandardowej serializacji.</span><span class="sxs-lookup"><span data-stu-id="c5de2-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="c5de2-232">Ma on toobe zserializowanym w formacie ciągu z ToString() lub używane z niestandardowych OUTPUTTER/WYODRĘBNIANIA.</span><span class="sxs-lookup"><span data-stu-id="c5de2-232">It either has toobe serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="c5de2-233">Teraz omówimy użycia UDT.</span><span class="sxs-lookup"><span data-stu-id="c5de2-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="c5de2-234">W sekcji związane z kodem możemy zmienić naszych GetFiscalPeriod funkcja toohello następujące:</span><span class="sxs-lookup"><span data-stu-id="c5de2-234">In a code-behind section, we changed our GetFiscalPeriod function toohello following:</span></span>

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

<span data-ttu-id="c5de2-235">Jak widać, zwraca wartość hello naszych FiscalPeriod typu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-235">As you can see, it returns hello value of our FiscalPeriod type.</span></span>

<span data-ttu-id="c5de2-236">W tym miejscu udostępniamy przykładowy sposób toouse dalsze w podstawowej skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c5de2-236">Here we provide an example of how toouse it further in U-SQL base script.</span></span> <span data-ttu-id="c5de2-237">W tym przykładzie przedstawiono różne formy UDT wywołanie skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c5de2-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

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

       // This user-defined type was created in hello prior SELECT.  Passing hello UDT toothis subsequent SELECT would have failed if hello UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="c5de2-238">Oto przykład pełnego kodem sekcji:</span><span class="sxs-lookup"><span data-stu-id="c5de2-238">Here's an example of a full code-behind section:</span></span>

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

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="c5de2-239">Użyj agregacje zdefiniowane przez użytkownika: UDAGG</span><span class="sxs-lookup"><span data-stu-id="c5de2-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="c5de2-240">Agregacje zdefiniowane przez użytkownika są wszystkie funkcje związane z agregacji, które są niewysłanych out-of--box języku U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c5de2-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="c5de2-241">przykład Witaj można agregacji tooperform obliczenia matematyczne niestandardowych, konkatenacji ciągów manipulacje z ciągami i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="c5de2-241">hello example can be an aggregate tooperform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="c5de2-242">Witaj użytkownika agregacji klasy podstawowej definicji jest następujący:</span><span class="sxs-lookup"><span data-stu-id="c5de2-242">hello user-defined aggregate base class definition is as follows:</span></span>

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

<span data-ttu-id="c5de2-243">**SqlUserDefinedAggregate** wskazuje, czy typ hello powinny być rejestrowane jako agregacji zdefiniowanej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5de2-243">**SqlUserDefinedAggregate** indicates that hello type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="c5de2-244">Ta klasa nie może być dziedziczona.</span><span class="sxs-lookup"><span data-stu-id="c5de2-244">This class cannot be inherited.</span></span>

<span data-ttu-id="c5de2-245">Atrybut SqlUserDefinedType jest **opcjonalne** UDAGG definicji.</span><span class="sxs-lookup"><span data-stu-id="c5de2-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="c5de2-246">Hello klasy podstawowej pozwala toopass trzy parametry abstrakcyjne: dwa jako parametry wejściowe i jeden hello wyniku.</span><span class="sxs-lookup"><span data-stu-id="c5de2-246">hello base class allows you toopass three abstract parameters: two as input parameters and one as hello result.</span></span> <span data-ttu-id="c5de2-247">typy danych Hello są zmienne i powinien być zdefiniowany podczas dziedziczenia klas.</span><span class="sxs-lookup"><span data-stu-id="c5de2-247">hello data types are variable and should be defined during class inheritance.</span></span>

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

* <span data-ttu-id="c5de2-248">**Init** wywołuje jeden raz dla każdej grupy podczas obliczania.</span><span class="sxs-lookup"><span data-stu-id="c5de2-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="c5de2-249">Procedura inicjowania zapewnia dla każdej grupy agregacji.</span><span class="sxs-lookup"><span data-stu-id="c5de2-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="c5de2-250">**Accumulate** jest wykonywane raz dla każdej wartości.</span><span class="sxs-lookup"><span data-stu-id="c5de2-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="c5de2-251">Zawiera funkcję main hello hello agregacji algorytmu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-251">It provides hello main functionality for hello aggregation algorithm.</span></span> <span data-ttu-id="c5de2-252">Może być używane tooaggregate wartości przy użyciu różnych typów danych zdefiniowanych podczas dziedziczenia klas.</span><span class="sxs-lookup"><span data-stu-id="c5de2-252">It can be used tooaggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="c5de2-253">Może akceptować dwa parametry o typach danych zmiennej.</span><span class="sxs-lookup"><span data-stu-id="c5de2-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="c5de2-254">**Przerwanie** jest wykonywane raz dla każdej grupy agregacji na końcu hello przetwarzania toooutput hello wynik dla każdej grupy.</span><span class="sxs-lookup"><span data-stu-id="c5de2-254">**Terminate** is executed once per aggregation group at hello end of processing toooutput hello result for each group.</span></span>

<span data-ttu-id="c5de2-255">toodeclare poprawne dane wejściowe i typów danych wyjściowych, użyj definicji klasy hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c5de2-255">toodeclare correct input and output data types, use hello class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="c5de2-256">T1: Pierwszy parametr tooaccumulate</span><span class="sxs-lookup"><span data-stu-id="c5de2-256">T1: First parameter tooaccumulate</span></span>
* <span data-ttu-id="c5de2-257">T2: Pierwszy parametr tooaccumulate</span><span class="sxs-lookup"><span data-stu-id="c5de2-257">T2: First parameter tooaccumulate</span></span>
* <span data-ttu-id="c5de2-258">TResult: Zwracany typ przerwania</span><span class="sxs-lookup"><span data-stu-id="c5de2-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="c5de2-259">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c5de2-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="c5de2-260">lub</span><span class="sxs-lookup"><span data-stu-id="c5de2-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="c5de2-261">Użyj UDAGG w języku U-SQL</span><span class="sxs-lookup"><span data-stu-id="c5de2-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="c5de2-262">toouse UDAGG, najpierw zdefiniować ją w CodeBehind lub Przywołaj ją z istniejących programowania hello biblioteki DLL, zgodnie z wcześniejszym opisem.</span><span class="sxs-lookup"><span data-stu-id="c5de2-262">toouse UDAGG, first define it in code-behind or reference it from hello existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="c5de2-263">Następnie hello użyj następującej składni:</span><span class="sxs-lookup"><span data-stu-id="c5de2-263">Then use hello following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="c5de2-264">Oto przykład UDAGG:</span><span class="sxs-lookup"><span data-stu-id="c5de2-264">Here is an example of UDAGG:</span></span>

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

<span data-ttu-id="c5de2-265">I podstawowego skryptu U-SQL:</span><span class="sxs-lookup"><span data-stu-id="c5de2-265">And base U-SQL script:</span></span>

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

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

<span data-ttu-id="c5de2-266">W tym scenariuszu przypadek użycia możemy łączenie identyfikatorów GUID klas hello określonych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c5de2-266">In this use-case scenario, we concatenate class GUIDs for hello specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="c5de2-267">Za pomocą obiektów zdefiniowanych przez użytkownika: UDO</span><span class="sxs-lookup"><span data-stu-id="c5de2-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="c5de2-268">U-SQL umożliwia toodefine programowania niestandardowych obiektów, które są nazywane obiekty zdefiniowane przez użytkownika lub UDO.</span><span class="sxs-lookup"><span data-stu-id="c5de2-268">U-SQL enables you toodefine custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="c5de2-269">Witaj poniżej znajduje się lista UDO w języku U-SQL:</span><span class="sxs-lookup"><span data-stu-id="c5de2-269">hello following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="c5de2-270">Ekstraktory zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="c5de2-270">User-defined extractors</span></span>
    * <span data-ttu-id="c5de2-271">Wyodrębnij wiersz po wierszu</span><span class="sxs-lookup"><span data-stu-id="c5de2-271">Extract row by row</span></span>
    * <span data-ttu-id="c5de2-272">Używane tooimplement wyodrębniania danych z niestandardowej strukturze plików</span><span class="sxs-lookup"><span data-stu-id="c5de2-272">Used tooimplement data extraction from custom structured files</span></span>

* <span data-ttu-id="c5de2-273">Outputters zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="c5de2-273">User-defined outputters</span></span>
    * <span data-ttu-id="c5de2-274">Dane wyjściowe wiersz po wierszu</span><span class="sxs-lookup"><span data-stu-id="c5de2-274">Output row by row</span></span>
    * <span data-ttu-id="c5de2-275">Używane toooutput niestandardowe typy danych lub niestandardowych formatów plików</span><span class="sxs-lookup"><span data-stu-id="c5de2-275">Used toooutput custom data types or custom file formats</span></span>

* <span data-ttu-id="c5de2-276">Procesory zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="c5de2-276">User-defined processors</span></span>
    * <span data-ttu-id="c5de2-277">Jeden wiersz i tworzące jeden wiersz</span><span class="sxs-lookup"><span data-stu-id="c5de2-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="c5de2-278">Używane tooreduce hello liczby kolumn lub utworzyć nowe kolumny z wartościami, które pochodzą z istniejącego zestawu kolumn</span><span class="sxs-lookup"><span data-stu-id="c5de2-278">Used tooreduce hello number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="c5de2-279">Appliers zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="c5de2-279">User-defined appliers</span></span>
    * <span data-ttu-id="c5de2-280">Jeden wiersz i tworzące 0 toon wierszy</span><span class="sxs-lookup"><span data-stu-id="c5de2-280">Take one row and produce 0 toon rows</span></span>
    * <span data-ttu-id="c5de2-281">Używane z Zastosuj zewnętrzne/między</span><span class="sxs-lookup"><span data-stu-id="c5de2-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="c5de2-282">Combiners zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="c5de2-282">User-defined combiners</span></span>
    * <span data-ttu-id="c5de2-283">Zestawy wierszy — sprzężenia zdefiniowane przez użytkownika łączy</span><span class="sxs-lookup"><span data-stu-id="c5de2-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="c5de2-284">Reduktory zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="c5de2-284">User-defined reducers</span></span>
    * <span data-ttu-id="c5de2-285">N wierszy i tworzące jeden wiersz</span><span class="sxs-lookup"><span data-stu-id="c5de2-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="c5de2-286">Używane tooreduce hello liczbę wierszy</span><span class="sxs-lookup"><span data-stu-id="c5de2-286">Used tooreduce hello number of rows</span></span>

<span data-ttu-id="c5de2-287">UDO jest zwykle nazywany jawnie skryptu U-SQL w ramach powitania po instrukcji U-SQL:</span><span class="sxs-lookup"><span data-stu-id="c5de2-287">UDO is typically called explicitly in U-SQL script as part of hello following U-SQL statements:</span></span>

* <span data-ttu-id="c5de2-288">WYODRĘBNIJ</span><span class="sxs-lookup"><span data-stu-id="c5de2-288">EXTRACT</span></span>
* <span data-ttu-id="c5de2-289">DANE WYJŚCIOWE</span><span class="sxs-lookup"><span data-stu-id="c5de2-289">OUTPUT</span></span>
* <span data-ttu-id="c5de2-290">PROCES</span><span class="sxs-lookup"><span data-stu-id="c5de2-290">PROCESS</span></span>
* <span data-ttu-id="c5de2-291">ŁĄCZENIE</span><span class="sxs-lookup"><span data-stu-id="c5de2-291">COMBINE</span></span>
* <span data-ttu-id="c5de2-292">ZMNIEJSZ</span><span class="sxs-lookup"><span data-stu-id="c5de2-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="c5de2-293">Dla obiektu UDO są ograniczone tooconsume 0,5 Gb pamięci.</span><span class="sxs-lookup"><span data-stu-id="c5de2-293">UDO’s are limited tooconsume 0.5Gb memory.</span></span>  <span data-ttu-id="c5de2-294">To ograniczenie pamięci nie ma zastosowania wykonaniami toolocal.</span><span class="sxs-lookup"><span data-stu-id="c5de2-294">This memory limitation does not apply toolocal executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="c5de2-295">Użyj ekstraktory zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="c5de2-295">Use user-defined extractors</span></span>
<span data-ttu-id="c5de2-296">U-SQL umożliwia tooimport danych zewnętrznych przy użyciu instrukcji WYODRĘBNIANIA.</span><span class="sxs-lookup"><span data-stu-id="c5de2-296">U-SQL allows you tooimport external data by using an EXTRACT statement.</span></span> <span data-ttu-id="c5de2-297">Instrukcja WYODRĘBNIANIA można użyć wbudowanych ekstraktory UDO:</span><span class="sxs-lookup"><span data-stu-id="c5de2-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="c5de2-298">*Extractors.Text()*: zapewnia wyodrębniania z plików tekstowych rozdzielanych różnych kodowań.</span><span class="sxs-lookup"><span data-stu-id="c5de2-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="c5de2-299">*Extractors.Csv()*: zapewnia wyodrębniania z wartościami rozdzielanymi przecinkami (CSV) plików różnych kodowań.</span><span class="sxs-lookup"><span data-stu-id="c5de2-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="c5de2-300">*Extractors.Tsv()*: zapewnia wyodrębniania z wartości tabulatorami (TSV) plików różnych kodowań.</span><span class="sxs-lookup"><span data-stu-id="c5de2-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="c5de2-301">Może to być przydatne toodevelop ekstraktor niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="c5de2-301">It can be useful toodevelop a custom extractor.</span></span> <span data-ttu-id="c5de2-302">Może to być przydatne podczas importowania danych, jeśli chcemy toodo żadnego hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="c5de2-302">This can be helpful during data import if we want toodo any of hello following tasks:</span></span>

* <span data-ttu-id="c5de2-303">Modyfikowanie danych wejściowych podział kolumn i modyfikując poszczególnych wartości.</span><span class="sxs-lookup"><span data-stu-id="c5de2-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="c5de2-304">Witaj funkcjonalność PROCESORA jest lepszym rozwiązaniem dla łączenie kolumn.</span><span class="sxs-lookup"><span data-stu-id="c5de2-304">hello PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="c5de2-305">Przeanalizować danych niestrukturalnych, takich jak strony sieci Web i wiadomości e-mail lub częściowo bez struktury danych, takich jak XML/JSON.</span><span class="sxs-lookup"><span data-stu-id="c5de2-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="c5de2-306">Analizować dane przy użyciu kodowania nieobsługiwany.</span><span class="sxs-lookup"><span data-stu-id="c5de2-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="c5de2-307">toodefine ekstraktor zdefiniowane przez użytkownika lub LUCZ, potrzebujemy toocreate `IExtractor` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-307">toodefine a user-defined extractor, or UDE, we need toocreate an `IExtractor` interface.</span></span> <span data-ttu-id="c5de2-308">Wszystkie dane wejściowe ekstraktor toohello parametry, takie jak ogranicznik wiersza/kolumny i kodowanie, muszą toobe zdefiniowane w Konstruktorze hello hello klasy.</span><span class="sxs-lookup"><span data-stu-id="c5de2-308">All input parameters toohello extractor, such as column/row delimiters, and encoding, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="c5de2-309">Witaj `IExtractor` interfejsu powinien również zawierać definicji hello `IEnumerable<IRow>` zastąpienia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c5de2-309">hello `IExtractor`  interface should also contain a definition for hello `IEnumerable<IRow>` override as follows:</span></span>

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

<span data-ttu-id="c5de2-310">Witaj **SqlUserDefinedExtractor** atrybut wskazuje, że typ hello powinny być rejestrowane jako ekstraktor zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5de2-310">hello **SqlUserDefinedExtractor** attribute indicates that hello type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="c5de2-311">Ta klasa nie może być dziedziczona.</span><span class="sxs-lookup"><span data-stu-id="c5de2-311">This class cannot be inherited.</span></span>

<span data-ttu-id="c5de2-312">SqlUserDefinedExtractor jest opcjonalny atrybut LUCZ definicji.</span><span class="sxs-lookup"><span data-stu-id="c5de2-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="c5de2-313">Właściwość AtomicFileProcessing toodefine on używany dla obiekt LUCZ hello.</span><span class="sxs-lookup"><span data-stu-id="c5de2-313">It used toodefine AtomicFileProcessing property for hello UDE object.</span></span>

* <span data-ttu-id="c5de2-314">wartość logiczna AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="c5de2-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="c5de2-315">**wartość true,** = wskazuje, że ta ekstraktor wymaga atomic plików wejściowych (JSON, XML,...)</span><span class="sxs-lookup"><span data-stu-id="c5de2-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="c5de2-316">**FALSE** = wskazuje, że ten ekstraktor można postępowania w przypadku plików podział / rozproszone (CSV, SEQ,...)</span><span class="sxs-lookup"><span data-stu-id="c5de2-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="c5de2-317">Witaj głównego LUCZ programowania obiekty są **wejściowych** i **dane wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="c5de2-317">hello main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="c5de2-318">obiekt wejściowy Hello jest używany tooenumerate danych wejściowych jako `IUnstructuredReader`.</span><span class="sxs-lookup"><span data-stu-id="c5de2-318">hello input object is used tooenumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="c5de2-319">Obiekt danych wyjściowych Hello jest używane tooset danych wyjściowych w wyniku działania ekstraktor hello.</span><span class="sxs-lookup"><span data-stu-id="c5de2-319">hello output object is used tooset output data as a result of hello extractor activity.</span></span>

<span data-ttu-id="c5de2-320">dane wejściowe Hello jest dostępny za pośrednictwem `System.IO.Stream` i `System.IO.StreamReader`.</span><span class="sxs-lookup"><span data-stu-id="c5de2-320">hello input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="c5de2-321">Wyliczenia kolumny wejściowe możemy najpierw podziału strumienia wejściowego hello przy użyciu ogranicznik wiersza.</span><span class="sxs-lookup"><span data-stu-id="c5de2-321">For input columns enumeration, we first split hello input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="c5de2-322">Następnie dodatkowo podzielić wejściowych wiersza części kolumny.</span><span class="sxs-lookup"><span data-stu-id="c5de2-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="c5de2-323">dane wyjściowe tooset, używamy hello `output.Set` metody.</span><span class="sxs-lookup"><span data-stu-id="c5de2-323">tooset output data, we use hello `output.Set` method.</span></span>

<span data-ttu-id="c5de2-324">Ważne toounderstand, który hello ekstraktor niestandardowych wyświetla tylko kolumny i wartości, które są zdefiniowane z danych wyjściowych hello jest.</span><span class="sxs-lookup"><span data-stu-id="c5de2-324">It's important toounderstand that hello custom extractor only outputs columns and values that are defined with hello output.</span></span> <span data-ttu-id="c5de2-325">Ustaw wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="c5de2-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="c5de2-326">dane wyjściowe rzeczywiste ekstraktor Hello jest wyzwalane przez wywołanie metody `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="c5de2-326">hello actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="c5de2-327">Przykład Witaj ekstraktor jest następujący:</span><span class="sxs-lookup"><span data-stu-id="c5de2-327">Following is hello extractor example:</span></span>

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
         //Read hello input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split hello input by hello column delimiter
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
                 // for column “user”, convert tooUPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep hello rest of hello columns as-is
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

<span data-ttu-id="c5de2-328">W tym scenariuszu przypadek użycia ekstraktor hello generuje hello identyfikatora GUID dla kolumny "guid" i konwertuje wartości hello przypadku tooupper kolumny "użytkownika".</span><span class="sxs-lookup"><span data-stu-id="c5de2-328">In this use-case scenario, hello extractor regenerates hello GUID for “guid” column and converts hello values of “user” column tooupper case.</span></span> <span data-ttu-id="c5de2-329">Niestandardowe ekstraktory może wygenerować bardziej skomplikowane wyniki analizy danych wejściowych i manipulowanie go.</span><span class="sxs-lookup"><span data-stu-id="c5de2-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="c5de2-330">Poniżej przedstawiono podstawowe skryptu U-SQL, który używa ekstraktor niestandardowych:</span><span class="sxs-lookup"><span data-stu-id="c5de2-330">Following is base U-SQL script that uses a custom extractor:</span></span>

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

OUTPUT @rs0 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a><span data-ttu-id="c5de2-331">Użyj outputters zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="c5de2-331">Use user-defined outputters</span></span>
<span data-ttu-id="c5de2-332">Zdefiniowane przez użytkownika outputter jest inny UDO U-SQL umożliwiająca tooextend wbudowanej funkcji U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c5de2-332">User-defined outputter is another U-SQL UDO that allows you tooextend built-in U-SQL functionality.</span></span> <span data-ttu-id="c5de2-333">Ekstraktor toohello podobne, istnieje kilka wbudowanych outputters.</span><span class="sxs-lookup"><span data-stu-id="c5de2-333">Similar toohello extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="c5de2-334">*Outputters.Text()*: zapisuje pliki tekstowe różnych kodowań toodelimited danych.</span><span class="sxs-lookup"><span data-stu-id="c5de2-334">*Outputters.Text()*: Writes data toodelimited text files of different encodings.</span></span>
* <span data-ttu-id="c5de2-335">*Outputters.Csv()*: zapisuje plik wartości rozdzielanych toocomma danych (CSV) plików różnych kodowań.</span><span class="sxs-lookup"><span data-stu-id="c5de2-335">*Outputters.Csv()*: Writes data toocomma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="c5de2-336">*Outputters.Tsv()*: zapisuje plik wartości rozdzielanych tootab danych plików (TSV) różnych kodowań.</span><span class="sxs-lookup"><span data-stu-id="c5de2-336">*Outputters.Tsv()*: Writes data tootab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="c5de2-337">Niestandardowe outputter umożliwia toowrite danych w niestandardowym formacie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="c5de2-337">Custom outputter allows you toowrite data in a custom defined format.</span></span> <span data-ttu-id="c5de2-338">Może to być przydatne w przypadku hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="c5de2-338">This can be useful for hello following tasks:</span></span>

* <span data-ttu-id="c5de2-339">Zapisywanie plików danych strukturalnych toosemi lub bez struktury.</span><span class="sxs-lookup"><span data-stu-id="c5de2-339">Writing data toosemi-structured or unstructured files.</span></span>
* <span data-ttu-id="c5de2-340">Zapisywanie danych nie obsługuje kodowania.</span><span class="sxs-lookup"><span data-stu-id="c5de2-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="c5de2-341">Modyfikowanie danych wyjściowych lub dodanie atrybutów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="c5de2-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="c5de2-342">toodefine outputter zdefiniowane przez użytkownika, potrzebujemy toocreate hello `IOutputter` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-342">toodefine user-defined outputter, we need toocreate hello `IOutputter` interface.</span></span>

<span data-ttu-id="c5de2-343">Poniżej przedstawiono podstawowe hello `IOutputter` Implementacja klasy:</span><span class="sxs-lookup"><span data-stu-id="c5de2-343">Following is hello base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="c5de2-344">Wszystkie dane wejściowe outputter toohello parametry, takie jak ogranicznik wiersza/kolumny, kodowanie i tak dalej, muszą toobe zdefiniowane w Konstruktorze hello hello klasy.</span><span class="sxs-lookup"><span data-stu-id="c5de2-344">All input parameters toohello outputter, such as column/row delimiters, encoding, and so on, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="c5de2-345">Witaj `IOutputter` interfejsu powinien również zawierać definicji `void Output` zastąpienia.</span><span class="sxs-lookup"><span data-stu-id="c5de2-345">hello `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="c5de2-346">Atrybut Hello `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` Opcjonalnie można ustawić dla przetwarzania plików atomic.</span><span class="sxs-lookup"><span data-stu-id="c5de2-346">hello attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="c5de2-347">Aby uzyskać więcej informacji zobacz hello poniższe informacje.</span><span class="sxs-lookup"><span data-stu-id="c5de2-347">For more information, see hello following details.</span></span>

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

* <span data-ttu-id="c5de2-348">`Output`jest wywoływana dla każdego wiersza wejściowego.</span><span class="sxs-lookup"><span data-stu-id="c5de2-348">`Output` is called for each input row.</span></span> <span data-ttu-id="c5de2-349">Zwraca hello `IUnstructuredWriter output` zestawu wierszy.</span><span class="sxs-lookup"><span data-stu-id="c5de2-349">It returns hello `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="c5de2-350">Konstruktor klasy Hello jest używany toopass parametry toohello outputter zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5de2-350">hello Constructor class is used toopass parameters toohello user-defined outputter.</span></span>
* <span data-ttu-id="c5de2-351">`Close`Służy toooptionally zastąpić stanu kosztowne toorelease lub określić, kiedy hello ostatni wiersz został zapisany.</span><span class="sxs-lookup"><span data-stu-id="c5de2-351">`Close` is used toooptionally override toorelease expensive state or determine when hello last row was written.</span></span>

<span data-ttu-id="c5de2-352">**SqlUserDefinedOutputter** atrybut wskazuje, że typ hello powinny być rejestrowane jako outputter zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5de2-352">**SqlUserDefinedOutputter** attribute indicates that hello type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="c5de2-353">Ta klasa nie może być dziedziczona.</span><span class="sxs-lookup"><span data-stu-id="c5de2-353">This class cannot be inherited.</span></span>

<span data-ttu-id="c5de2-354">SqlUserDefinedOutputter jest opcjonalny atrybut dla definicji outputter zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5de2-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="c5de2-355">Został on użyty toodefine hello AtomicFileProcessing właściwości.</span><span class="sxs-lookup"><span data-stu-id="c5de2-355">It's used toodefine hello AtomicFileProcessing property.</span></span>

* <span data-ttu-id="c5de2-356">wartość logiczna AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="c5de2-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="c5de2-357">**wartość true,** = wskazuje, że ten outputter wymaga pliki wyjściowe niepodzielne (JSON, XML,...)</span><span class="sxs-lookup"><span data-stu-id="c5de2-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="c5de2-358">**FALSE** = wskazuje, że ten outputter można postępowania w przypadku plików podział / rozproszone (CSV, SEQ,...)</span><span class="sxs-lookup"><span data-stu-id="c5de2-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="c5de2-359">Obiekty główne programowania Hello są **wiersza** i **dane wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="c5de2-359">hello main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="c5de2-360">Witaj **wiersza** obiekt jest używany tooenumerate dane wyjściowe jako `IRow` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-360">hello **row** object is used tooenumerate output data as `IRow` interface.</span></span> <span data-ttu-id="c5de2-361">**Dane wyjściowe** jest pliku docelowego toohello danych wyjściowych tooset używane.</span><span class="sxs-lookup"><span data-stu-id="c5de2-361">**Output** is used tooset output data toohello target file.</span></span>

<span data-ttu-id="c5de2-362">Witaj danych wyjściowych jest dostępny za pośrednictwem hello `IRow` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-362">hello output data is accessed through hello `IRow` interface.</span></span> <span data-ttu-id="c5de2-363">Dane wyjściowe są przekazywane wiersza w czasie.</span><span class="sxs-lookup"><span data-stu-id="c5de2-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="c5de2-364">Witaj poszczególne wartości wyliczane są przez wywołanie metody Get hello interfejsu IRow hello:</span><span class="sxs-lookup"><span data-stu-id="c5de2-364">hello individual values are enumerated by calling hello Get method of hello IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="c5de2-365">Można ustalić nazwy poszczególnych kolumn przez wywołanie metody `row.Schema`:</span><span class="sxs-lookup"><span data-stu-id="c5de2-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="c5de2-366">Takie podejście umożliwia toobuild elastyczne outputter dla żadnego schematu metadanych.</span><span class="sxs-lookup"><span data-stu-id="c5de2-366">This approach enables you toobuild a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="c5de2-367">Witaj dane wyjściowe są zapisywane toofile przy użyciu `System.IO.StreamWriter`.</span><span class="sxs-lookup"><span data-stu-id="c5de2-367">hello output data is written toofile by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="c5de2-368">Parametr strumienia Hello ustawiono zbyt`output.BaseStrea` jako część `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="c5de2-368">hello stream parameter is set too`output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="c5de2-369">Należy pamiętać, że ważne tooflush hello danych buforu toohello pliku po każdej iteracji wiersza.</span><span class="sxs-lookup"><span data-stu-id="c5de2-369">Note that it's important tooflush hello data buffer toohello file after each row iteration.</span></span> <span data-ttu-id="c5de2-370">Ponadto hello `StreamWriter` atrybutem hello jednorazowe włączone (ustawienie domyślne) i hello, można użyć obiektu **przy użyciu** — słowo kluczowe:</span><span class="sxs-lookup"><span data-stu-id="c5de2-370">In addition, hello `StreamWriter` object must be used with hello Disposable attribute enabled (default) and with hello **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="c5de2-371">W przeciwnym razie wywołanie metody Flush() jawnie po każdej iteracji.</span><span class="sxs-lookup"><span data-stu-id="c5de2-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="c5de2-372">Ten zostanie przedstawiony w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="c5de2-372">We show this in hello following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="c5de2-373">Ustaw nagłówki i stopki dla outputter zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="c5de2-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="c5de2-374">tooset nagłówka Użyj jednego iteracji wykonywania przepływu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-374">tooset a header, use single iteration execution flow.</span></span>

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

<span data-ttu-id="c5de2-375">najpierw Hello kodu w hello `if (isHeaderRow)` bloku jest wykonywane tylko raz.</span><span class="sxs-lookup"><span data-stu-id="c5de2-375">hello code in hello first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="c5de2-376">Stopki hello, należy użyć wystąpienia toohello odwołanie hello `System.IO.Stream` obiektu (`output.BaseStream`).</span><span class="sxs-lookup"><span data-stu-id="c5de2-376">For hello footer, use hello reference toohello instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="c5de2-377">Zapisywanie hello stopki w hello metody Close() hello `IOutputter` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-377">Write hello footer in hello Close() method of hello `IOutputter` interface.</span></span>  <span data-ttu-id="c5de2-378">(Aby uzyskać więcej informacji, zobacz poniższy przykład hello).</span><span class="sxs-lookup"><span data-stu-id="c5de2-378">(For more information, see hello following example.)</span></span>

<span data-ttu-id="c5de2-379">Poniżej przedstawiono przykład outputter zdefiniowane przez użytkownika:</span><span class="sxs-lookup"><span data-stu-id="c5de2-379">Following is an example of a user-defined outputter:</span></span>

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

    // hello Close method is used toowrite hello footer toohello file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference tooIO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization tooenumerate column names
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
        // Data type enumeration--required toomatch hello distinct list of types from OUTPUT statement
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
    // Reference toohello instance of hello IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define hello factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

<span data-ttu-id="c5de2-380">I podstawowy skrypt U-SQL:</span><span class="sxs-lookup"><span data-stu-id="c5de2-380">And U-SQL base script:</span></span>

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
    too@output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="c5de2-381">Jest to outputter HTML, który tworzy plik HTML z danych tabeli.</span><span class="sxs-lookup"><span data-stu-id="c5de2-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="c5de2-382">Wywołanie outputter z podstawowej skryptu U-SQL</span><span class="sxs-lookup"><span data-stu-id="c5de2-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="c5de2-383">toocall niestandardowych outputter z podstawowej skryptu U-SQL hello hello nowe wystąpienie obiektu outputter hello ma toobe utworzony.</span><span class="sxs-lookup"><span data-stu-id="c5de2-383">toocall a custom outputter from hello base U-SQL script, hello new instance of hello outputter object has toobe created.</span></span>

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="c5de2-384">tooavoid tworzenia wystąpienia hello obiektów w skrypcie podstawowej, można utworzyć otoki funkcji, jak pokazano w naszym przykładzie wcześniej:</span><span class="sxs-lookup"><span data-stu-id="c5de2-384">tooavoid creating an instance of hello object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

```c#
        // Define hello factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

<span data-ttu-id="c5de2-385">W takim przypadku wywołania oryginalnego hello wygląda hello:</span><span class="sxs-lookup"><span data-stu-id="c5de2-385">In this case, hello original call looks like hello following:</span></span>

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="c5de2-386">Używają procesorów zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="c5de2-386">Use user-defined processors</span></span>
<span data-ttu-id="c5de2-387">Procesor zdefiniowane przez użytkownika lub UDP, jest typem obiektu UDO U-SQL, umożliwiający tooprocess hello przychodzących wierszy, stosując funkcje programowania.</span><span class="sxs-lookup"><span data-stu-id="c5de2-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you tooprocess hello incoming rows by applying programmability features.</span></span> <span data-ttu-id="c5de2-388">UDP umożliwia toocombine kolumny, zmodyfikuj wartości, a w razie potrzeby należy dodać nowe kolumny.</span><span class="sxs-lookup"><span data-stu-id="c5de2-388">UDP enables you toocombine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="c5de2-389">Zasadniczo pomaga tooprocess elementy danych tooproduce wymagany zestaw wierszy.</span><span class="sxs-lookup"><span data-stu-id="c5de2-389">Basically, it helps tooprocess a rowset tooproduce required data elements.</span></span>

<span data-ttu-id="c5de2-390">toodefine UDP, potrzebujemy toocreate `IProcessor` interfejsu z hello `SqlUserDefinedProcessor` atrybut, który jest opcjonalne dla protokołu UDP.</span><span class="sxs-lookup"><span data-stu-id="c5de2-390">toodefine a UDP, we need toocreate an `IProcessor` interface with hello `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="c5de2-391">Ten interfejs musi zawierać definicję hello na powitania `IRow` zastąpić interfejsu zestawu wierszy, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="c5de2-391">This interface should contain hello definition for hello `IRow` interface rowset override, as shown in hello following example:</span></span>

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

<span data-ttu-id="c5de2-392">**SqlUserDefinedProcessor** wskazuje, że hello typu powinny być rejestrowane jako procesor zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5de2-392">**SqlUserDefinedProcessor** indicates that hello type should be registered as a user-defined processor.</span></span> <span data-ttu-id="c5de2-393">Ta klasa nie może być dziedziczona.</span><span class="sxs-lookup"><span data-stu-id="c5de2-393">This class cannot be inherited.</span></span>

<span data-ttu-id="c5de2-394">Atrybut SqlUserDefinedProcessor Hello jest **opcjonalne** dla definicji UDP.</span><span class="sxs-lookup"><span data-stu-id="c5de2-394">hello SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="c5de2-395">Obiekty główne programowania Hello są **wejściowych** i **dane wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="c5de2-395">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="c5de2-396">obiekt wejściowy Hello jest kolumny wejściowe używane tooenumerate i wyjścia i danych wyjściowych tooset wyniku hello aktywności procesora.</span><span class="sxs-lookup"><span data-stu-id="c5de2-396">hello input object is used tooenumerate input columns and output, and tooset output data as a result of hello processor activity.</span></span>

<span data-ttu-id="c5de2-397">Wyliczenia kolumny wejściowe używamy hello `input.Get` metody.</span><span class="sxs-lookup"><span data-stu-id="c5de2-397">For input columns enumeration, we use hello `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="c5de2-398">Witaj parametr `input.Get` kolumny, która jest przekazywany jako część hello jest metoda `PRODUCE` klauzuli hello `PROCESS` instrukcji podstawowy skrypt hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c5de2-398">hello parameter for `input.Get` method is a column that's passed as part of hello `PRODUCE` clause of hello `PROCESS` statement of hello U-SQL base script.</span></span> <span data-ttu-id="c5de2-399">Potrzebujemy toouse hello poprawne dane wpisz tekst tutaj.</span><span class="sxs-lookup"><span data-stu-id="c5de2-399">We need toouse hello correct data type here.</span></span>

<span data-ttu-id="c5de2-400">Dla danych wyjściowych, użyj hello `output.Set` metody.</span><span class="sxs-lookup"><span data-stu-id="c5de2-400">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="c5de2-401">Ważne jest toonote tej niestandardowej producent wyświetla tylko kolumny i wartości, które są zdefiniowane z hello `output.Set` wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="c5de2-401">It's important toonote that custom producer only outputs columns and values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="c5de2-402">dane wyjściowe procesora rzeczywistych Hello jest wyzwalane przez wywołanie metody `return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="c5de2-402">hello actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="c5de2-403">Poniżej przedstawiono przykład procesora:</span><span class="sxs-lookup"><span data-stu-id="c5de2-403">Following is a processor example:</span></span>

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

<span data-ttu-id="c5de2-404">W tym scenariuszu przypadek użycia procesora hello generuje nową kolumnę o nazwie "full_description" łącząc hello istniejące kolumny — w tym przypadku "użytkownika" wielkimi literami i "des".</span><span class="sxs-lookup"><span data-stu-id="c5de2-404">In this use-case scenario, hello processor is generating a new column called “full_description” by combining hello existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="c5de2-405">Również generuje identyfikator GUID i zwraca hello oryginalnego i nowej wartości identyfikatora GUID.</span><span class="sxs-lookup"><span data-stu-id="c5de2-405">It also regenerates a GUID and returns hello original and new GUID values.</span></span>

<span data-ttu-id="c5de2-406">Jak widać w poprzednim przykładzie hello, należy wywołać metodę C# podczas `output.Set` wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="c5de2-406">As you can see from hello previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="c5de2-407">Poniżej przedstawiono przykład podstawowego skryptu U-SQL, który używa niestandardowego procesora:</span><span class="sxs-lookup"><span data-stu-id="c5de2-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

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

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a><span data-ttu-id="c5de2-408">Użyj appliers zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="c5de2-408">Use user-defined appliers</span></span>
<span data-ttu-id="c5de2-409">U-SQL applier zdefiniowane przez użytkownika umożliwia funkcja tooinvoke niestandardowych C# dla każdego wiersza, który jest zwracany przez hello Tabela zewnętrzna wyrażenie zapytania.</span><span class="sxs-lookup"><span data-stu-id="c5de2-409">A U-SQL user-defined applier enables you tooinvoke a custom C# function for each row that's returned by hello outer table expression of a query.</span></span> <span data-ttu-id="c5de2-410">dane wejściowe Hello jest obliczane dla każdego wiersza z powitania po lewej stronie dane wejściowe i hello wierszy, które są tworzone są łączone na powitania ostateczne dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c5de2-410">hello right input is evaluated for each row from hello left input, and hello rows that are produced are combined for hello final output.</span></span> <span data-ttu-id="c5de2-411">Hello listy kolumn, które są tworzone przez operatora APPLY hello są kombinacją hello hello zestawu kolumn w lewo hello i hello prawo danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="c5de2-411">hello list of columns that are produced by hello APPLY operator are hello combination of hello set of columns in hello left and hello right input.</span></span>

<span data-ttu-id="c5de2-412">Zdefiniowane przez użytkownika applier jest wywoływany jako część hello wybierz USQL wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="c5de2-412">User-defined applier is being invoked as part of hello USQL SELECT expression.</span></span>

<span data-ttu-id="c5de2-413">Typowy Hello wywołania toohello użytkownika applier prawdopodobnie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="c5de2-413">hello typical call toohello user-defined applier looks like hello following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="c5de2-414">Aby uzyskać więcej informacji o używaniu appliers w wyrażeniu SELECT, zobacz [U-SQL wybierz wybrać między Zastosuj i zewnętrzne](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span><span class="sxs-lookup"><span data-stu-id="c5de2-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="c5de2-415">Witaj użytkownika applier klasy podstawowej definicji jest następujący:</span><span class="sxs-lookup"><span data-stu-id="c5de2-415">hello user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="c5de2-416">toodefine applier zdefiniowane przez użytkownika, potrzebujemy toocreate hello `IApplier` interfejsu z hello [`SqlUserDefinedApplier`] atrybut, który jest opcjonalne dla definicji applier zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5de2-416">toodefine a user-defined applier, we need toocreate hello `IApplier` interface with hello [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

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

* <span data-ttu-id="c5de2-417">Zastosuj jest wywoływana dla każdego wiersza tabeli zewnętrznej hello.</span><span class="sxs-lookup"><span data-stu-id="c5de2-417">Apply is called for each row of hello outer table.</span></span> <span data-ttu-id="c5de2-418">Zwraca hello `IUpdatableRow` output zestawu wierszy.</span><span class="sxs-lookup"><span data-stu-id="c5de2-418">It returns hello `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="c5de2-419">Hello Konstruktor klasy jest używane toopass parametry toohello applier zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5de2-419">hello Constructor class is used toopass parameters toohello user-defined applier.</span></span>

<span data-ttu-id="c5de2-420">**SqlUserDefinedApplier** wskazuje, czy typ hello powinny być rejestrowane jako applier zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5de2-420">**SqlUserDefinedApplier** indicates that hello type should be registered as a user-defined applier.</span></span> <span data-ttu-id="c5de2-421">Ta klasa nie może być dziedziczona.</span><span class="sxs-lookup"><span data-stu-id="c5de2-421">This class cannot be inherited.</span></span>

<span data-ttu-id="c5de2-422">**SqlUserDefinedApplier** jest **opcjonalne** dla definicji applier zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5de2-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="c5de2-423">Obiekty główne programowania Hello są następujące:</span><span class="sxs-lookup"><span data-stu-id="c5de2-423">hello main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="c5de2-424">Wejściowe zestawy wierszy są przekazywane jako `IRow` wejściowego.</span><span class="sxs-lookup"><span data-stu-id="c5de2-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="c5de2-425">Witaj wierszy dane wyjściowe są generowane jako `IUpdatableRow` interfejsu danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c5de2-425">hello output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="c5de2-426">Można ustalić nazwy poszczególnych kolumn przy hello wywoływania `IRow` metody schematu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-426">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="c5de2-427">tooget hello rzeczywistych wartości danych z hello przychodzące `IRow`, możemy użyć metody Get() hello `IRow` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-427">tooget hello actual data values from hello incoming `IRow`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="c5de2-428">Lub używamy nazwy kolumny schematu hello:</span><span class="sxs-lookup"><span data-stu-id="c5de2-428">Or we use hello schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="c5de2-429">Witaj dane wyjściowe należy ustawić wartości z `IUpdatableRow` danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="c5de2-429">hello output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="c5de2-430">Jest ważne toounderstand, że niestandardowe appliers output tylko kolumny i wartości, które są zdefiniowane z `output.Set` wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="c5de2-430">It is important toounderstand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="c5de2-431">rzeczywiste dane wyjściowe Hello jest wyzwalane przez wywołanie metody `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="c5de2-431">hello actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="c5de2-432">Hello użytkownika applier parametry mogą być przekazywane toohello konstruktora.</span><span class="sxs-lookup"><span data-stu-id="c5de2-432">hello user-defined applier parameters can be passed toohello constructor.</span></span> <span data-ttu-id="c5de2-433">Applier może zwracać zmienną liczbę kolumn, które wymagają toobe zdefiniowane podczas wywołania applier hello w podstawowej skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c5de2-433">Applier can return a variable number of columns that need toobe defined during hello applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="c5de2-434">Oto przykład applier użytkownika hello:</span><span class="sxs-lookup"><span data-stu-id="c5de2-434">Here is hello user-defined applier example:</span></span>

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

<span data-ttu-id="c5de2-435">Hello podstawowej skryptu U-SQL dla tego użytkownika applier jest następujący:</span><span class="sxs-lookup"><span data-stu-id="c5de2-435">Following is hello base U-SQL script for this user-defined applier:</span></span>

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

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

<span data-ttu-id="c5de2-436">W tym scenariuszem użycia, zdefiniowane przez użytkownika applier działa jako wartości rozdzielane przecinkami analizatora składni właściwości floty samochodów hello.</span><span class="sxs-lookup"><span data-stu-id="c5de2-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for hello car fleet properties.</span></span> <span data-ttu-id="c5de2-437">wiersze pliku wejściowego Hello wyglądać hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c5de2-437">hello input file rows look like hello following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="c5de2-438">Jest to typowe tabulacji TSV plik z kolumną właściwości zawierającego właściwości samochodu, takich jak marka i model.</span><span class="sxs-lookup"><span data-stu-id="c5de2-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="c5de2-439">Te właściwości muszą być analizowany toohello kolumn tabeli.</span><span class="sxs-lookup"><span data-stu-id="c5de2-439">Those properties must be parsed toohello table columns.</span></span> <span data-ttu-id="c5de2-440">applier Hello, który został dostarczony umożliwia również toogenerate dynamiczne liczba właściwości w hello powoduje zestawu wierszy, na podstawie parametru hello, która została przekazana.</span><span class="sxs-lookup"><span data-stu-id="c5de2-440">hello applier that's provided also enables you toogenerate a dynamic number of properties in hello result rowset, based on hello parameter that's passed.</span></span> <span data-ttu-id="c5de2-441">Można wygenerować właściwości wszystkich lub określonych tylko właściwości.</span><span class="sxs-lookup"><span data-stu-id="c5de2-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="c5de2-442">Witaj applier zdefiniowane przez użytkownika można wywołać jako nowe wystąpienie obiektu applier:</span><span class="sxs-lookup"><span data-stu-id="c5de2-442">hello user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="c5de2-443">Lub wywołanie metody fabryki otoki hello:</span><span class="sxs-lookup"><span data-stu-id="c5de2-443">Or with hello invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="c5de2-444">Użyj combiners zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="c5de2-444">Use user-defined combiners</span></span>
<span data-ttu-id="c5de2-445">Zdefiniowane przez użytkownika łączenia lub UDC, umożliwia toocombine wiersze z lewego i prawego zestawów wierszy, opartych na logice niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="c5de2-445">User-defined combiner, or UDC, enables you toocombine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="c5de2-446">Zdefiniowane przez użytkownika łączenia jest używany z łączenia wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="c5de2-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="c5de2-447">Łączenia jest wywoływany z hello łączenie wyrażenie, które zawiera hello niezbędne informacje na temat zestawów wierszy zarówno hello wejściowych, grupowanie kolumn, hello hello oczekiwany wynik schematu i dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="c5de2-447">A combiner is being invoked with hello COMBINE expression that provides hello necessary information about both hello input rowsets, hello grouping columns, hello expected result schema, and additional information.</span></span>

<span data-ttu-id="c5de2-448">toocall łączenia w podstawowej skryptu U-SQL, stosujemy hello następującej składni:</span><span class="sxs-lookup"><span data-stu-id="c5de2-448">toocall a combiner in a base U-SQL script, we use hello following syntax:</span></span>

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

<span data-ttu-id="c5de2-449">Aby uzyskać więcej informacji, zobacz [łączenia wyrażenia (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span><span class="sxs-lookup"><span data-stu-id="c5de2-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="c5de2-450">toodefine łączenia zdefiniowane przez użytkownika, potrzebujemy toocreate hello `ICombiner` interfejsu z hello [`SqlUserDefinedCombiner`] atrybut, który jest opcjonalne dla definicji łączenia zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5de2-450">toodefine a user-defined combiner, we need toocreate hello `ICombiner` interface with hello [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="c5de2-451">Podstawa `ICombiner` definicji klasy:</span><span class="sxs-lookup"><span data-stu-id="c5de2-451">Base `ICombiner` class definition:</span></span>

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

<span data-ttu-id="c5de2-452">Witaj niestandardowej implementacji `ICombiner` interfejsu powinny zawierać definicji hello `IEnumerable<IRow>` połączyć zastąpienie.</span><span class="sxs-lookup"><span data-stu-id="c5de2-452">hello custom implementation of an `ICombiner` interface should contain hello definition for an `IEnumerable<IRow>` Combine override.</span></span>

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

<span data-ttu-id="c5de2-453">Witaj **SqlUserDefinedCombiner** atrybut wskazuje, że typ hello powinny być rejestrowane jako łączenia zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5de2-453">hello **SqlUserDefinedCombiner** attribute indicates that hello type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="c5de2-454">Ta klasa nie może być dziedziczona.</span><span class="sxs-lookup"><span data-stu-id="c5de2-454">This class cannot be inherited.</span></span>

<span data-ttu-id="c5de2-455">**SqlUserDefinedCombiner** jest używane toodefine hello łączenia tryb właściwości.</span><span class="sxs-lookup"><span data-stu-id="c5de2-455">**SqlUserDefinedCombiner** is used toodefine hello Combiner mode property.</span></span> <span data-ttu-id="c5de2-456">Jest opcjonalny atrybut dla definicji łączenia zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5de2-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="c5de2-457">Tryb CombinerMode</span><span class="sxs-lookup"><span data-stu-id="c5de2-457">CombinerMode     Mode</span></span>

<span data-ttu-id="c5de2-458">Wyliczenia CombinerMode może zająć hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="c5de2-458">CombinerMode enum can take hello following values:</span></span>

* <span data-ttu-id="c5de2-459">Pełny (0), każdy wiersz danych wyjściowych zależy od potencjalnie wszystkie wiersze danych wejściowych powitania od lewej i prawej z hello sama wartość klucza.</span><span class="sxs-lookup"><span data-stu-id="c5de2-459">Full  (0) Every output row potentially depends on all hello input rows from left and right       with hello same key value.</span></span>

* <span data-ttu-id="c5de2-460">Każdy wiersz danych wyjściowych jest zależna od pojedynczy wiersz wejściowych od lewej hello lewej strony (1) (i potencjalnie wszystkie wiersze z tabeli hello prawo z hello sama wartość klucza).</span><span class="sxs-lookup"><span data-stu-id="c5de2-460">Left  (1) Every output row depends on a single input row from hello left (and potentially all rows       from hello right with hello same key value).</span></span>

* <span data-ttu-id="c5de2-461">Każdy wiersz danych wyjściowych jest zależna od pojedynczy wiersz wejściowych z prawej hello prawo [2] (i potencjalnie wszystkie wiersze z tabeli po lewej hello z hello sama wartość klucza).</span><span class="sxs-lookup"><span data-stu-id="c5de2-461">Right (2)     Every output row depends on a single input row from hello right (and potentially all rows       from hello left with hello same key value).</span></span>

* <span data-ttu-id="c5de2-462">Wewnętrzny (3) każdy wiersz danych wyjściowych zależy od pojedynczego danych wejściowych wiersza w lewo i prawo z hello takie same wartości.</span><span class="sxs-lookup"><span data-stu-id="c5de2-462">Inner (3) Every output row depends on a single input row from left and right with hello same value.</span></span>

<span data-ttu-id="c5de2-463">Przykład: [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="c5de2-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="c5de2-464">Obiekty główne programowania Hello są:</span><span class="sxs-lookup"><span data-stu-id="c5de2-464">hello main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="c5de2-465">Wejściowe zestawy wierszy są przekazywane jako **po lewej stronie** i **prawo** `IRowset` typ interfejsu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="c5de2-466">Oba zestawy wierszy musi zostać wyliczone do przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="c5de2-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="c5de2-467">Można tylko wyliczyć każdy interfejs, dlatego firma Microsoft ma tooenumerate i jego pamięci podręcznej, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c5de2-467">You can only enumerate each interface once, so we have tooenumerate and cache it if necessary.</span></span>

<span data-ttu-id="c5de2-468">Na potrzeby buforowania, można utworzyć listy\<T\> typ konstrukcji pamięci w związku z tym składnika LINQ wykonywanie zapytania, w szczególności listę <`IRow`>.</span><span class="sxs-lookup"><span data-stu-id="c5de2-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="c5de2-469">Typ anonimowy danych Hello może służyć podczas wyliczania również.</span><span class="sxs-lookup"><span data-stu-id="c5de2-469">hello anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="c5de2-470">Zobacz [wprowadzenie tooLINQ kwerend (C#)](https://msdn.microsoft.com/library/bb397906.aspx) uzyskać więcej informacji dotyczących zapytań LINQ i [IEnumerable\<T\> interfejsu](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) Aby uzyskać więcej informacji na temat interfejsu IEnumerable\<T\> interfejsu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-470">See [Introduction tooLINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="c5de2-471">tooget hello rzeczywistych wartości danych z hello przychodzące `IRowset`, możemy użyć metody Get() hello `IRow` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-471">tooget hello actual data values from hello incoming `IRowset`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="c5de2-472">Można ustalić nazwy poszczególnych kolumn przy hello wywoływania `IRow` metody schematu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-472">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="c5de2-473">Lub za pomocą nazwy kolumny schematu hello:</span><span class="sxs-lookup"><span data-stu-id="c5de2-473">Or by using hello schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="c5de2-474">Wyliczenie ogólne Hello za pomocą LINQ wygląda hello:</span><span class="sxs-lookup"><span data-stu-id="c5de2-474">hello general enumeration with LINQ looks like hello following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="c5de2-475">Po wyliczania oba zestawy wierszy, zamierzamy tooloop za pośrednictwem wszystkich wierszy.</span><span class="sxs-lookup"><span data-stu-id="c5de2-475">After enumerating both rowsets, we are going tooloop through all rows.</span></span> <span data-ttu-id="c5de2-476">Dla każdego wiersza w zestawie wierszy po lewej stronie powitania zamierzamy toofind wszystkie wiersze, które spełniają warunek hello naszych łączenia.</span><span class="sxs-lookup"><span data-stu-id="c5de2-476">For each row in hello left rowset, we are going toofind all rows that satisfy hello condition of our combiner.</span></span>

<span data-ttu-id="c5de2-477">Witaj dane wyjściowe należy ustawić wartości z `IUpdatableRow` danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c5de2-477">hello output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="c5de2-478">rzeczywiste dane wyjściowe Hello jest wyzwalany przez wywołanie za`yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="c5de2-478">hello actual output is triggered by calling too`yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="c5de2-479">Poniżej przedstawiono przykład łączenia:</span><span class="sxs-lookup"><span data-stu-id="c5de2-479">Following is a combiner example:</span></span>

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

<span data-ttu-id="c5de2-480">W tym scenariuszu przypadek użycia możemy tworzenia raportu analizy dla detalicznej hello.</span><span class="sxs-lookup"><span data-stu-id="c5de2-480">In this use-case scenario, we are building an analytics report for hello retailer.</span></span> <span data-ttu-id="c5de2-481">Celem Hello jest toofind wszystkie produkty, których koszt ponad 20 000 $ i że sprzedaży za pośrednictwem witryny sieci Web hello jest szybsza niż sprzedaży detalicznej regularne hello w danym okresie.</span><span class="sxs-lookup"><span data-stu-id="c5de2-481">hello goal is toofind all products that cost more than $20,000 and that sell through hello website faster than through hello regular retailer within a certain time frame.</span></span>

<span data-ttu-id="c5de2-482">Oto hello podstawowy skrypt U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c5de2-482">Here is hello base U-SQL script.</span></span> <span data-ttu-id="c5de2-483">Możesz porównać logiki hello między sprzężenia regularnego i łączenia:</span><span class="sxs-lookup"><span data-stu-id="c5de2-483">You can compare hello logic between a regular JOIN and a combiner:</span></span>

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

OUTPUT @rs1 too@output_file1 USING Outputters.Tsv();
OUTPUT @rs2 too@output_file2 USING Outputters.Tsv();
```

<span data-ttu-id="c5de2-484">Zdefiniowane przez użytkownika łączenia można wywołać jako nowe wystąpienie obiektu applier hello:</span><span class="sxs-lookup"><span data-stu-id="c5de2-484">A user-defined combiner can be called as a new instance of hello applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="c5de2-485">Lub wywołanie metody fabryki otoki hello:</span><span class="sxs-lookup"><span data-stu-id="c5de2-485">Or with hello invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="c5de2-486">Użyj reduktory zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="c5de2-486">Use user-defined reducers</span></span>

<span data-ttu-id="c5de2-487">U-SQL umożliwia toowrite reduktory niestandardowego zestawu wierszy w języku C# z wykorzystaniem strukturę rozszerzalności zdefiniowany przez użytkownika operator hello i implementowanie interfejsu IReducer.</span><span class="sxs-lookup"><span data-stu-id="c5de2-487">U-SQL enables you toowrite custom rowset reducers in C# by using hello user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="c5de2-488">Reduktor zdefiniowane przez użytkownika lub przez, może być niepotrzebne wierszy tooeliminate używane podczas wyodrębniania danych (Importuj).</span><span class="sxs-lookup"><span data-stu-id="c5de2-488">User-defined reducer, or UDR, can be used tooeliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="c5de2-489">Jego również używane toomanipulate i ocenić, wierszy i kolumn.</span><span class="sxs-lookup"><span data-stu-id="c5de2-489">It also can be used toomanipulate and evaluate rows and columns.</span></span> <span data-ttu-id="c5de2-490">Opartych na logice programowania, jego można również zdefiniować wiersze, które wymagają toobe wyodrębnione.</span><span class="sxs-lookup"><span data-stu-id="c5de2-490">Based on programmability logic, it can also define which rows need toobe extracted.</span></span>

<span data-ttu-id="c5de2-491">toodefine przez klasę, potrzebujemy toocreate `IReducer` interfejsu z opcjonalną `SqlUserDefinedReducer` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="c5de2-491">toodefine a UDR class, we need toocreate an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="c5de2-492">Ten interfejs klasy powinny zawierać definicji hello `IEnumerable` zastąpienie interfejsu zestawu wierszy.</span><span class="sxs-lookup"><span data-stu-id="c5de2-492">This class interface should contain a definition for hello `IEnumerable` interface rowset override.</span></span>

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

<span data-ttu-id="c5de2-493">Witaj **SqlUserDefinedReducer** atrybut wskazuje, że typ hello powinny być rejestrowane jako reduktor zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5de2-493">hello **SqlUserDefinedReducer** attribute indicates that hello type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="c5de2-494">Ta klasa nie może być dziedziczona.</span><span class="sxs-lookup"><span data-stu-id="c5de2-494">This class cannot be inherited.</span></span>
<span data-ttu-id="c5de2-495">**SqlUserDefinedReducer** jest opcjonalny atrybut dla definicji reduktor zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5de2-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="c5de2-496">Został on użyty toodefine IsRecursive właściwości.</span><span class="sxs-lookup"><span data-stu-id="c5de2-496">It's used toodefine IsRecursive property.</span></span>

* <span data-ttu-id="c5de2-497">wartość logiczna IsRecursive</span><span class="sxs-lookup"><span data-stu-id="c5de2-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="c5de2-498">**wartość true,** = wskazuje, czy ta reduktor jest idempotentności</span><span class="sxs-lookup"><span data-stu-id="c5de2-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="c5de2-499">Obiekty główne programowania Hello są **wejściowych** i **dane wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="c5de2-499">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="c5de2-500">obiekt wejściowy Hello jest używane tooenumerate wiersze danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="c5de2-500">hello input object is used tooenumerate input rows.</span></span> <span data-ttu-id="c5de2-501">Dane wyjściowe są używane tooset wiersze danych wyjściowych wyniku zmniejszenie działania.</span><span class="sxs-lookup"><span data-stu-id="c5de2-501">Output is used tooset output rows as a result of reducing activity.</span></span>

<span data-ttu-id="c5de2-502">Wyliczenia wiersze danych wejściowych używamy hello `Row.Get` metody.</span><span class="sxs-lookup"><span data-stu-id="c5de2-502">For input rows enumeration, we use hello `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="c5de2-503">Witaj parametr hello `Row.Get` kolumny, która jest przekazywany jako część hello jest metoda `PRODUCE` klasy hello `REDUCE` instrukcji podstawowy skrypt hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c5de2-503">hello parameter for hello `Row.Get` method is a column that's passed as part of hello `PRODUCE` class of hello `REDUCE` statement of hello U-SQL base script.</span></span> <span data-ttu-id="c5de2-504">Potrzebujemy toouse hello poprawne dane w tym miejscu wpisz również.</span><span class="sxs-lookup"><span data-stu-id="c5de2-504">We need toouse hello correct data type here as well.</span></span>

<span data-ttu-id="c5de2-505">Dla danych wyjściowych, użyj hello `output.Set` metody.</span><span class="sxs-lookup"><span data-stu-id="c5de2-505">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="c5de2-506">Jest ważne toounderstand, który hello niestandardowych reduktor tylko dane wyjściowe wartości, które są zdefiniowane z `output.Set` wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="c5de2-506">It is important toounderstand that custom reducer only outputs values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="c5de2-507">dane wyjściowe rzeczywiste reduktor Hello jest wyzwalane przez wywołanie metody `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="c5de2-507">hello actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="c5de2-508">Poniżej przedstawiono przykład reduktor:</span><span class="sxs-lookup"><span data-stu-id="c5de2-508">Following is a reducer example:</span></span>

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

<span data-ttu-id="c5de2-509">W tym scenariuszu przypadek użycia reduktor hello pomija wiersze z Pusta nazwa użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5de2-509">In this use-case scenario, hello reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="c5de2-510">Dla każdego wiersza w zestawie wierszy go odczytuje każdej wymaganej kolumny, a następnie oblicza długość hello hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5de2-510">For each row in rowset, it reads each required column, then evaluates hello length of hello user name.</span></span> <span data-ttu-id="c5de2-511">Rzeczywiste wiersza hello go generuje tylko wtedy, gdy długość wartości nazwy użytkownika jest większa niż 0.</span><span class="sxs-lookup"><span data-stu-id="c5de2-511">It outputs hello actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="c5de2-512">Poniżej przedstawiono podstawowy skryptu U-SQL, który używa niestandardowych reduktor:</span><span class="sxs-lookup"><span data-stu-id="c5de2-512">Following is base U-SQL script that uses a custom reducer:</span></span>

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
    too@output_file 
    USING Outputters.Text();
```
