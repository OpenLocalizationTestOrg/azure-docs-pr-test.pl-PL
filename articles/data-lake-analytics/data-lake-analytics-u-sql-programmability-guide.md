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
# <a name="u-sql-programmability-guide"></a>Podręcznik programowania U-SQL

U-SQL jest język zapytania, które jest przeznaczone do typów danych dużych obciążeń. Jednym z hello funkcji U-SQL jest hello kombinację hello deklaratywne języka przypominającego SQL o rozszerzalności hello i programowania, który znajduje się w języku C#. W tym przewodniku możemy skupić się na powitania rozszerzania i programowania hello języka U-SQL, który został włączony w języku C#.

## <a name="requirements"></a>Wymagania

Pobierz i zainstaluj [Azure Data Lake Tools dla programu Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

## <a name="get-started-with-u-sql"></a>Wprowadzenie do języka U-SQL  

Przyjrzyjmy się hello następującego skryptu U-SQL:

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

Definiuje zestawu wierszy o nazwie @a i tworzy zestawu wierszy o nazwie @results z @a.

## <a name="c-types-and-expressions-in-u-sql-script"></a>Typy C# i wyrażenia w skryptu U-SQL

Wyrażenie U-SQL jest wyrażenie C# połączone z operacji logicznych U-SQL takich `AND`, `OR`, i `NOT`. Wyrażenia języka U-SQL mogą być używane z SELECT, EXTRACT, gdzie wystąpienia, Grupuj według, ZADEKLAROWAĆ.

Na przykład hello następującego skryptu analizuje ciąg, wartość daty i godziny w klauzuli SELECT hello.

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

Witaj poniższy skrypt analizuje ciąg wartość daty i godziny w instrukcji DECLARE.

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a>Używanie wyrażeń C# dla konwersje typów danych
Witaj poniższy przykład pokazuje, jak data/godzina konwersji danych za pomocą wyrażeń C#. W tym scenariuszu określonego danych dotyczących ciągu daty/godziny to data i godzina przekonwertowanego toostandard o północy 00:00:00 czasu notacji.

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a>Używanie wyrażeń C# dla bieżącej daty
toopull dzisiaj, możemy użyć powitania po wyrażeniu C#:

```
DateTime.Now.ToString("M/d/yyyy")
```

Poniżej przedstawiono przykładowy sposób toouse tego wyrażenia w skrypcie:

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



## <a name="using-net-assemblies"></a>Za pomocą zestawów platformy .NET
U-SQL modelu rozszerzalności odgrywa hello możliwości tooadd niestandardowego kodu. Obecnie U-SQL zapewnia łatwy sposób tooadd własnych firmy Microsoft. Kod na podstawie sieci (w szczególności, C#). Jednak można również dodać kodu niestandardowego, który jest zapisywany w innych językach .NET, takie jak VB.NET lub F #. 

### <a name="register-a-net-assembly"></a>Rejestrowanie zestawów platformy .NET

Użyj hello utworzyć zestaw instrukcji tooplace zestaw .NET do języka U-SQL bazy danych. Po zestaw znajduje się w bazie danych, w skryptów U-SQL przy użyciu instrukcji zestaw odwołania hello można użyć tych zestawów. 

Witaj następującego kodu pokazuje sposób tooregister zestawu:

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

Witaj następującego kodu pokazuje sposób tooreference zestawu:

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

Zapoznaj się hello [instrukcje rejestracji zestawu](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) który obejmuje w tym temacie bardziej szczegółowo.


### <a name="use-assembly-versioning"></a>Użyj wersji zestawu
Obecnie U-SQL używa hello .NET Framework w wersji 4.5. Dlatego upewnij się, że własne zestawy są zgodne z tą wersją środowiska uruchomieniowego hello.

Jak wspomniano wcześniej, kod działa U-SQL w formacie 64-bitowej (x 64). Dlatego upewnij się, że kod jest skompilowany toorun na x64. W przeciwnym razie błąd hello niepoprawny format przedstawiona wcześniej.

Każdy przekazany zestaw biblioteki DLL i pliku zasobów, takich jak innego środowiska uruchomieniowego, natywny zestaw lub pliku konfiguracji, może mieć maksymalnie 400 MB. Całkowity rozmiar Hello wdrożonych zasobów za pomocą wdrażania zasobów lub za pośrednictwem tooassemblies odwołań i dodatkowe pliki, nie może przekraczać 3 GB.

Na koniec należy pamiętać, że każda baza danych U-SQL może zawierać tylko jedną wersję żadnych danego zestawu. Na przykład, jeśli potrzebujesz zarówno w wersji 7, jak i w wersji 8 hello biblioteki NewtonSoft Json.Net, należy tooregister w dwóch różnych baz danych. Ponadto każdy skrypt może odwoływać się tylko wersję tooone danego zestawu biblioteki DLL. W związku z tym U-SQL następuje hello C# zestawu zarządzania i wersji semantyki.


## <a name="use-user-defined-functions-udf"></a>Użyj funkcji zdefiniowanej przez użytkownika: funkcji zdefiniowanej przez użytkownika
Funkcje zdefiniowane przez użytkownika U-SQL lub funkcji zdefiniowanej przez użytkownika, są programowania procedur, które akceptują parametrów, wykonywania akcji (na przykład złożonych obliczeń) i zwraca wynik hello tego działania jako wartość. Witaj zwracać wartość funkcji zdefiniowanej przez użytkownika może być tylko jeden skalarnej. UDF języka U-SQL może zostać wywołany w podstawowej skryptu U-SQL, takich jak wszystkie inne C# skalarną.

Firma Microsoft zaleca, aby zainicjować U-SQL funkcje zdefiniowane przez użytkownika jako **publicznego** i **statycznych**.

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

Pierwszy Przyjrzyjmy się hello prosty przykład tworzenia funkcji zdefiniowanej przez użytkownika.

W tym scenariuszu przypadek użycia potrzebujemy toodetermine hello okres, w tym hello kwartał i miesiąc obrachunkowy hello pierwszego logowania dla określonego użytkownika hello. Witaj pierwszy miesiąc obrachunkowy roku hello w naszym scenariuszu jest czerwca.

okres toocalculate wprowadzeniu powitania po funkcji języka C#:

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

Po prostu oblicza miesiąc obrachunkowy i kwartał i zwraca wartość typu ciąg. Czerwca, hello pierwszy miesiąc hello pierwszy kwartał używamy "Q1:P1". Lipca możemy użyć "Q1:P2" i tak dalej.

To normalne działanie C# pracujemy toouse będzie w naszym projektu U-SQL.

Poniżej przedstawiono wygląd hello związane z kodem sekcji w tym scenariuszu:

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

Teraz zamierzamy toocall tej funkcji z hello podstawowy skrypt U-SQL. toodo, mamy tooprovide w pełni kwalifikowanej nazwy funkcji hello, włącznie z przestrzenią nazw hello, czyli w tym przypadku NameSpace.Class.Function(parameter).

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

Rzeczywiste skrypt bazowy hello U-SQL jest następujący:

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

Plik wyjściowy hello wykonywania skryptów hello jest następujący:

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

W tym przykładzie przedstawiono prosty użycie wbudowanej funkcji zdefiniowanej przez użytkownika w języku U-SQL.

### <a name="keep-state-between-udf-invocations"></a>Zachowaj stanu między wywołań funkcji zdefiniowanej przez użytkownika
Obiekty programowania U-SQL C# można można bardziej zaawansowane opcje, wykorzystując interakcyjności za pomocą zmiennych globalnych hello związane z kodem. Przyjrzyjmy się powitania po scenariusza biznesowego przypadek użycia.

W dużych organizacjach użytkownicy mogą przełączać odmian wewnętrznych aplikacji. Obejmują one programu Microsoft Dynamics CRM, usługa Power Bi i tak dalej. Klienci mogą też chcieć tooapply analizy telemetrii sposób użytkownicy będą przełączać się między różnymi aplikacjami, jakie użycia hello trendy są i tak dalej. Celem Hello dla firm hello jest toooptimize użycia aplikacji. Są też toocombine różnych aplikacji lub określonych procedur logowania jednokrotnego.

tooachieve tego celu, będziemy mieć identyfikatory sesji toodetermine i czas opóźnienia między hello ostatniej sesji, który wystąpił.

Firma Microsoft muszą toofind poprzedniego logowanie, a następnie przypisz tej sesji logowania tooall, które są generowane toohello tej samej aplikacji. pierwszego wyzwania Hello jest, że podstawowy skrypt U-SQL nie zezwala na nam obliczeń tooapply za pośrednictwem już obliczane kolumny z funkcja LAG. Witaj drugi wyzwaniem jest czy mamy tookeep hello określonej sesji dla wszystkich sesji w ramach hello sam okres czasu.

toosolve ten problem, używamy zmiennej globalnej wewnątrz sekcji CodeBehind: `static public string globalSession;`.

Tę zmienną globalną jest stosowane toohello całego zestawu wierszy podczas wykonywania naszych skryptu.

Oto hello związane z kodem sekcji nasz program U-SQL:

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

W tym przykładzie przedstawiono hello zmiennej globalnej `static public string globalSession;` używany wewnątrz hello `getStampUserSession` funkcji i uzyskiwanie za każdego hello czasu sesji parametr zostanie zmieniona.

Witaj podstawowy skrypt U-SQL jest następujący:

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

Funkcja `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` jest tutaj wywoływana podczas obliczania wierszy pamięci drugi hello. Przekazuje ono hello `UserSessionTimestamp` kolumny i zwraca wartość, dopóki hello `UserSessionTimestamp` została zmieniona.

Plik wyjściowy Hello jest następujący:

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

W tym przykładzie przedstawiono bardziej skomplikowane scenariusz przypadek użycia, w której używamy zmiennej globalnej wewnątrz sekcji związane z kodem, która jest stosowane toohello całej pamięci wierszy.

## <a name="use-user-defined-types-udt"></a>Używanie typów zdefiniowanych przez użytkownika: UDT
Typy definiowane przez użytkownika lub UDT, jest inna funkcja programowalności U-SQL. UDT U-SQL zachowuje się jak zwykły C# zdefiniowane przez użytkownika typu. C# to silnie typizowaną język, który umożliwia wykorzystanie hello wbudowane i niestandardowe typy danych zdefiniowane przez użytkownika.

U-SQL nie można niejawnie serializacji lub zdeserializować dowolnego UDTs podczas przekazywania hello UDT między wierzchołków w zestawów wierszy. Oznacza to, że hello, które użytkownik ma tooprovide jawne elementu formatującego za pomocą interfejsu IFormatter hello. Zapewnia to U-SQL z hello serializacji i deserializacji metody hello UDT.

> [!NOTE]
> U-SQL ekstraktory wbudowanych i outputters obecnie nie można serializować lub zdeserializować UDT tooor danych z plików, nawet w przypadku hello IFormatter zestawu. Dlatego podczas pisania pliku tooa danych UDT hello danych wyjściowych instrukcji lub odczytywania go z katalogu, możesz mieć toopass go w formie ciągu lub tablicy typu byte. Następnie wywołaj hello serializacji i deserializacji kodu (to znaczy metodę ToString() hello UDT) jawnie. Zdefiniowane przez użytkownika ekstraktory outputters na powitania innych ręcznie, może Odczyt i zapis typów.

Jeśli chcesz ponowić toouse UDT w katalogu lub OUTPUTTER (Brak poprzedniej wybierz), jak pokazano poniżej:

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

Otrzymaliśmy hello następujący błąd:

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

toowork z UDT w outputter albo mamy tooserialize on toostring z hello metodę ToString() lub Utwórz niestandardowe outputter.

Typów nie można obecnie używać w GROUP BY. Jeśli UDT jest używany w GROUP BY, jest zgłaszany hello następujący błąd:

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

toodefine UDT, konieczne jest:

* Dodaj następujące obszary nazw hello:

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* Dodaj `Microsoft.Analytics.Interfaces`, co jest wymagane dla interfejsów UDT hello. Ponadto `System.IO` może być wymagane toodefine hello IFormatter interfejsu.

* Zdefiniuj typ zdefiniowane z atrybutem SqlUserDefinedType.

**SqlUserDefinedType** jest definicją typu w zestawie co typ zdefiniowany przez użytkownika (UDT) toomark używanych w języku U-SQL. właściwości Hello atrybutu hello odzwierciedlają hello charakterystyki fizycznej hello UDT. Ta klasa nie może być dziedziczona.

SqlUserDefinedType jest wymagany atrybut UDT definicji.

Witaj konstruktora klasy hello:  

* SqlUserDefinedTypeAttribute (elementu formatującego typu)

* Program formatujący typ: wymagany parametr toodefine program formatujący UDT — w szczególności hello typu hello `IFormatter` interfejsu muszą być przekazywane w tym miejscu.

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* Typowy UDT wymaga również definicji interfejsu IFormatter hello, jak pokazano w hello poniższy przykład:

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

Witaj `IFormatter` interfejsu serializuje i zwalnia serializuje wykres obiektu typu głównego hello \<typeparamref name = "T" >.

\<typeparam name = "T" > Witaj typu głównego dla tooserialize wykresu obiektu hello i zdeserializować.

* **Deserializacja**: cofnąć serializuje dane hello w strumieniu hello podane i reconstitutes hello wykresu obiektów.

* **Serializować**: Serializuje obiekt lub grafu obiektów, z hello danego strumienia toohello podane głównego.

`MyType`wystąpienie: wystąpienie typu hello.  
`IColumnWriter`Moduł zapisujący / `IColumnReader` czytnika: hello bazowy strumieniu kolumny.  
`ISerializationContext`kontekst: wyliczenia, który definiuje zestaw flagi określa hello źródłowy lub docelowy kontekst dla strumienia hello podczas serializacji.

* **Pośredni**: Określa kontekst tego hello źródłowy lub docelowy nie jest utrwalonego magazynu.

* **Trwałość**: Określa kontekst tego hello źródłowy lub docelowy jest utrwalonego magazynu.

Jako regularne C# typ, definicji UDT U-SQL mogą zawierać zastąpień dla operatorów takich jak +/ == /! =. Może również obejmować metod statycznych. Na przykład, jeśli zamierzamy toouse tego UDT jako tooa parametru funkcji agregującej MIN U-SQL, mamy toodefine < zastąpienie operatora.

Wcześniej w tym przewodniku firma Microsoft przedstawiono przykład obrachunkowym identyfikacji okresu od określonej daty hello w formacie hello Qn:Pn (Q1:P10). Witaj poniższy przykład pokazuje, jak toodefine niestandardowego typu wartości okresu obrachunkowym.

Poniżej przedstawiono przykład sekcji kodu powiązanego z niestandardowy interfejs UDT i IFormatter:

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

Witaj zdefiniowanego typu zawiera dwie liczb: kwartał i miesiąc. Operatory == /! = / > / < a statyczną metodę ToString() są zdefiniowane w tym miejscu.

Jak wspomniano wcześniej, można używać w wyrażeniach wybierz UDT, ale nie można używać w OUTPUTTER/EKSTRAKTOR bez niestandardowej serializacji. Ma on toobe zserializowanym w formacie ciągu z ToString() lub używane z niestandardowych OUTPUTTER/WYODRĘBNIANIA.

Teraz omówimy użycia UDT. W sekcji związane z kodem możemy zmienić naszych GetFiscalPeriod funkcja toohello następujące:

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

Jak widać, zwraca wartość hello naszych FiscalPeriod typu.

W tym miejscu udostępniamy przykładowy sposób toouse dalsze w podstawowej skryptu U-SQL. W tym przykładzie przedstawiono różne formy UDT wywołanie skryptu U-SQL.

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

Oto przykład pełnego kodem sekcji:

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

## <a name="use-user-defined-aggregates-udagg"></a>Użyj agregacje zdefiniowane przez użytkownika: UDAGG
Agregacje zdefiniowane przez użytkownika są wszystkie funkcje związane z agregacji, które są niewysłanych out-of--box języku U-SQL. przykład Witaj można agregacji tooperform obliczenia matematyczne niestandardowych, konkatenacji ciągów manipulacje z ciągami i tak dalej.

Witaj użytkownika agregacji klasy podstawowej definicji jest następujący:

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

**SqlUserDefinedAggregate** wskazuje, czy typ hello powinny być rejestrowane jako agregacji zdefiniowanej przez użytkownika. Ta klasa nie może być dziedziczona.

Atrybut SqlUserDefinedType jest **opcjonalne** UDAGG definicji.


Hello klasy podstawowej pozwala toopass trzy parametry abstrakcyjne: dwa jako parametry wejściowe i jeden hello wyniku. typy danych Hello są zmienne i powinien być zdefiniowany podczas dziedziczenia klas.

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

* **Init** wywołuje jeden raz dla każdej grupy podczas obliczania. Procedura inicjowania zapewnia dla każdej grupy agregacji.  
* **Accumulate** jest wykonywane raz dla każdej wartości. Zawiera funkcję main hello hello agregacji algorytmu. Może być używane tooaggregate wartości przy użyciu różnych typów danych zdefiniowanych podczas dziedziczenia klas. Może akceptować dwa parametry o typach danych zmiennej.
* **Przerwanie** jest wykonywane raz dla każdej grupy agregacji na końcu hello przetwarzania toooutput hello wynik dla każdej grupy.

toodeclare poprawne dane wejściowe i typów danych wyjściowych, użyj definicji klasy hello w następujący sposób:

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* T1: Pierwszy parametr tooaccumulate
* T2: Pierwszy parametr tooaccumulate
* TResult: Zwracany typ przerwania

Na przykład:

```
public class GuidAggregate : IAggregate<string, int, int>
```

lub

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a>Użyj UDAGG w języku U-SQL
toouse UDAGG, najpierw zdefiniować ją w CodeBehind lub Przywołaj ją z istniejących programowania hello biblioteki DLL, zgodnie z wcześniejszym opisem.

Następnie hello użyj następującej składni:

```
AGG<UDAGG_functionname>(param1,param2)
```

Oto przykład UDAGG:

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

I podstawowego skryptu U-SQL:

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

W tym scenariuszu przypadek użycia możemy łączenie identyfikatorów GUID klas hello określonych użytkowników.

## <a name="use-user-defined-objects-udo"></a>Za pomocą obiektów zdefiniowanych przez użytkownika: UDO
U-SQL umożliwia toodefine programowania niestandardowych obiektów, które są nazywane obiekty zdefiniowane przez użytkownika lub UDO.

Witaj poniżej znajduje się lista UDO w języku U-SQL:

* Ekstraktory zdefiniowane przez użytkownika
    * Wyodrębnij wiersz po wierszu
    * Używane tooimplement wyodrębniania danych z niestandardowej strukturze plików

* Outputters zdefiniowane przez użytkownika
    * Dane wyjściowe wiersz po wierszu
    * Używane toooutput niestandardowe typy danych lub niestandardowych formatów plików

* Procesory zdefiniowane przez użytkownika
    * Jeden wiersz i tworzące jeden wiersz
    * Używane tooreduce hello liczby kolumn lub utworzyć nowe kolumny z wartościami, które pochodzą z istniejącego zestawu kolumn

* Appliers zdefiniowane przez użytkownika
    * Jeden wiersz i tworzące 0 toon wierszy
    * Używane z Zastosuj zewnętrzne/między

* Combiners zdefiniowane przez użytkownika
    * Zestawy wierszy — sprzężenia zdefiniowane przez użytkownika łączy

* Reduktory zdefiniowane przez użytkownika
    * N wierszy i tworzące jeden wiersz
    * Używane tooreduce hello liczbę wierszy

UDO jest zwykle nazywany jawnie skryptu U-SQL w ramach powitania po instrukcji U-SQL:

* WYODRĘBNIJ
* DANE WYJŚCIOWE
* PROCES
* ŁĄCZENIE
* ZMNIEJSZ

> [!NOTE]  
> Dla obiektu UDO są ograniczone tooconsume 0,5 Gb pamięci.  To ograniczenie pamięci nie ma zastosowania wykonaniami toolocal.

## <a name="use-user-defined-extractors"></a>Użyj ekstraktory zdefiniowane przez użytkownika
U-SQL umożliwia tooimport danych zewnętrznych przy użyciu instrukcji WYODRĘBNIANIA. Instrukcja WYODRĘBNIANIA można użyć wbudowanych ekstraktory UDO:  

* *Extractors.Text()*: zapewnia wyodrębniania z plików tekstowych rozdzielanych różnych kodowań.

* *Extractors.Csv()*: zapewnia wyodrębniania z wartościami rozdzielanymi przecinkami (CSV) plików różnych kodowań.

* *Extractors.Tsv()*: zapewnia wyodrębniania z wartości tabulatorami (TSV) plików różnych kodowań.

Może to być przydatne toodevelop ekstraktor niestandardowych. Może to być przydatne podczas importowania danych, jeśli chcemy toodo żadnego hello następujące zadania:

* Modyfikowanie danych wejściowych podział kolumn i modyfikując poszczególnych wartości. Witaj funkcjonalność PROCESORA jest lepszym rozwiązaniem dla łączenie kolumn.
* Przeanalizować danych niestrukturalnych, takich jak strony sieci Web i wiadomości e-mail lub częściowo bez struktury danych, takich jak XML/JSON.
* Analizować dane przy użyciu kodowania nieobsługiwany.

toodefine ekstraktor zdefiniowane przez użytkownika lub LUCZ, potrzebujemy toocreate `IExtractor` interfejsu. Wszystkie dane wejściowe ekstraktor toohello parametry, takie jak ogranicznik wiersza/kolumny i kodowanie, muszą toobe zdefiniowane w Konstruktorze hello hello klasy. Witaj `IExtractor` interfejsu powinien również zawierać definicji hello `IEnumerable<IRow>` zastąpienia w następujący sposób:

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

Witaj **SqlUserDefinedExtractor** atrybut wskazuje, że typ hello powinny być rejestrowane jako ekstraktor zdefiniowane przez użytkownika. Ta klasa nie może być dziedziczona.

SqlUserDefinedExtractor jest opcjonalny atrybut LUCZ definicji. Właściwość AtomicFileProcessing toodefine on używany dla obiekt LUCZ hello.

* wartość logiczna AtomicFileProcessing   

* **wartość true,** = wskazuje, że ta ekstraktor wymaga atomic plików wejściowych (JSON, XML,...)
* **FALSE** = wskazuje, że ten ekstraktor można postępowania w przypadku plików podział / rozproszone (CSV, SEQ,...)

Witaj głównego LUCZ programowania obiekty są **wejściowych** i **dane wyjściowe**. obiekt wejściowy Hello jest używany tooenumerate danych wejściowych jako `IUnstructuredReader`. Obiekt danych wyjściowych Hello jest używane tooset danych wyjściowych w wyniku działania ekstraktor hello.

dane wejściowe Hello jest dostępny za pośrednictwem `System.IO.Stream` i `System.IO.StreamReader`.

Wyliczenia kolumny wejściowe możemy najpierw podziału strumienia wejściowego hello przy użyciu ogranicznik wiersza.

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

Następnie dodatkowo podzielić wejściowych wiersza części kolumny.

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

dane wyjściowe tooset, używamy hello `output.Set` metody.

Ważne toounderstand, który hello ekstraktor niestandardowych wyświetla tylko kolumny i wartości, które są zdefiniowane z danych wyjściowych hello jest. Ustaw wywołania metody.

```
output.Set<string>(count, part);
```

dane wyjściowe rzeczywiste ekstraktor Hello jest wyzwalane przez wywołanie metody `yield return output.AsReadOnly();`.

Przykład Witaj ekstraktor jest następujący:

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

W tym scenariuszu przypadek użycia ekstraktor hello generuje hello identyfikatora GUID dla kolumny "guid" i konwertuje wartości hello przypadku tooupper kolumny "użytkownika". Niestandardowe ekstraktory może wygenerować bardziej skomplikowane wyniki analizy danych wejściowych i manipulowanie go.

Poniżej przedstawiono podstawowe skryptu U-SQL, który używa ekstraktor niestandardowych:

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

## <a name="use-user-defined-outputters"></a>Użyj outputters zdefiniowane przez użytkownika
Zdefiniowane przez użytkownika outputter jest inny UDO U-SQL umożliwiająca tooextend wbudowanej funkcji U-SQL. Ekstraktor toohello podobne, istnieje kilka wbudowanych outputters.

* *Outputters.Text()*: zapisuje pliki tekstowe różnych kodowań toodelimited danych.
* *Outputters.Csv()*: zapisuje plik wartości rozdzielanych toocomma danych (CSV) plików różnych kodowań.
* *Outputters.Tsv()*: zapisuje plik wartości rozdzielanych tootab danych plików (TSV) różnych kodowań.

Niestandardowe outputter umożliwia toowrite danych w niestandardowym formacie zdefiniowane. Może to być przydatne w przypadku hello następujące zadania:

* Zapisywanie plików danych strukturalnych toosemi lub bez struktury.
* Zapisywanie danych nie obsługuje kodowania.
* Modyfikowanie danych wyjściowych lub dodanie atrybutów niestandardowych.

toodefine outputter zdefiniowane przez użytkownika, potrzebujemy toocreate hello `IOutputter` interfejsu.

Poniżej przedstawiono podstawowe hello `IOutputter` Implementacja klasy:

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

Wszystkie dane wejściowe outputter toohello parametry, takie jak ogranicznik wiersza/kolumny, kodowanie i tak dalej, muszą toobe zdefiniowane w Konstruktorze hello hello klasy. Witaj `IOutputter` interfejsu powinien również zawierać definicji `void Output` zastąpienia. Atrybut Hello `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` Opcjonalnie można ustawić dla przetwarzania plików atomic. Aby uzyskać więcej informacji zobacz hello poniższe informacje.

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

* `Output`jest wywoływana dla każdego wiersza wejściowego. Zwraca hello `IUnstructuredWriter output` zestawu wierszy.
* Konstruktor klasy Hello jest używany toopass parametry toohello outputter zdefiniowane przez użytkownika.
* `Close`Służy toooptionally zastąpić stanu kosztowne toorelease lub określić, kiedy hello ostatni wiersz został zapisany.

**SqlUserDefinedOutputter** atrybut wskazuje, że typ hello powinny być rejestrowane jako outputter zdefiniowane przez użytkownika. Ta klasa nie może być dziedziczona.

SqlUserDefinedOutputter jest opcjonalny atrybut dla definicji outputter zdefiniowane przez użytkownika. Został on użyty toodefine hello AtomicFileProcessing właściwości.

* wartość logiczna AtomicFileProcessing   

* **wartość true,** = wskazuje, że ten outputter wymaga pliki wyjściowe niepodzielne (JSON, XML,...)
* **FALSE** = wskazuje, że ten outputter można postępowania w przypadku plików podział / rozproszone (CSV, SEQ,...)

Obiekty główne programowania Hello są **wiersza** i **dane wyjściowe**. Witaj **wiersza** obiekt jest używany tooenumerate dane wyjściowe jako `IRow` interfejsu. **Dane wyjściowe** jest pliku docelowego toohello danych wyjściowych tooset używane.

Witaj danych wyjściowych jest dostępny za pośrednictwem hello `IRow` interfejsu. Dane wyjściowe są przekazywane wiersza w czasie.

Witaj poszczególne wartości wyliczane są przez wywołanie metody Get hello interfejsu IRow hello:

```
row.Get<string>("column_name")
```

Można ustalić nazwy poszczególnych kolumn przez wywołanie metody `row.Schema`:

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

Takie podejście umożliwia toobuild elastyczne outputter dla żadnego schematu metadanych.

Witaj dane wyjściowe są zapisywane toofile przy użyciu `System.IO.StreamWriter`. Parametr strumienia Hello ustawiono zbyt`output.BaseStrea` jako część `IUnstructuredWriter output`.

Należy pamiętać, że ważne tooflush hello danych buforu toohello pliku po każdej iteracji wiersza. Ponadto hello `StreamWriter` atrybutem hello jednorazowe włączone (ustawienie domyślne) i hello, można użyć obiektu **przy użyciu** — słowo kluczowe:

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

W przeciwnym razie wywołanie metody Flush() jawnie po każdej iteracji. Ten zostanie przedstawiony w hello poniższy przykład.

### <a name="set-headers-and-footers-for-user-defined-outputter"></a>Ustaw nagłówki i stopki dla outputter zdefiniowane przez użytkownika
tooset nagłówka Użyj jednego iteracji wykonywania przepływu.

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

najpierw Hello kodu w hello `if (isHeaderRow)` bloku jest wykonywane tylko raz.

Stopki hello, należy użyć wystąpienia toohello odwołanie hello `System.IO.Stream` obiektu (`output.BaseStream`). Zapisywanie hello stopki w hello metody Close() hello `IOutputter` interfejsu.  (Aby uzyskać więcej informacji, zobacz poniższy przykład hello).

Poniżej przedstawiono przykład outputter zdefiniowane przez użytkownika:

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

I podstawowy skrypt U-SQL:

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

Jest to outputter HTML, który tworzy plik HTML z danych tabeli.

### <a name="call-outputter-from-u-sql-base-script"></a>Wywołanie outputter z podstawowej skryptu U-SQL
toocall niestandardowych outputter z podstawowej skryptu U-SQL hello hello nowe wystąpienie obiektu outputter hello ma toobe utworzony.

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

tooavoid tworzenia wystąpienia hello obiektów w skrypcie podstawowej, można utworzyć otoki funkcji, jak pokazano w naszym przykładzie wcześniej:

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

W takim przypadku wywołania oryginalnego hello wygląda hello:

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a>Używają procesorów zdefiniowane przez użytkownika
Procesor zdefiniowane przez użytkownika lub UDP, jest typem obiektu UDO U-SQL, umożliwiający tooprocess hello przychodzących wierszy, stosując funkcje programowania. UDP umożliwia toocombine kolumny, zmodyfikuj wartości, a w razie potrzeby należy dodać nowe kolumny. Zasadniczo pomaga tooprocess elementy danych tooproduce wymagany zestaw wierszy.

toodefine UDP, potrzebujemy toocreate `IProcessor` interfejsu z hello `SqlUserDefinedProcessor` atrybut, który jest opcjonalne dla protokołu UDP.

Ten interfejs musi zawierać definicję hello na powitania `IRow` zastąpić interfejsu zestawu wierszy, jak pokazano w hello poniższy przykład:

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

**SqlUserDefinedProcessor** wskazuje, że hello typu powinny być rejestrowane jako procesor zdefiniowane przez użytkownika. Ta klasa nie może być dziedziczona.

Atrybut SqlUserDefinedProcessor Hello jest **opcjonalne** dla definicji UDP.

Obiekty główne programowania Hello są **wejściowych** i **dane wyjściowe**. obiekt wejściowy Hello jest kolumny wejściowe używane tooenumerate i wyjścia i danych wyjściowych tooset wyniku hello aktywności procesora.

Wyliczenia kolumny wejściowe używamy hello `input.Get` metody.

```
string column_name = input.Get<string>("column_name");
```

Witaj parametr `input.Get` kolumny, która jest przekazywany jako część hello jest metoda `PRODUCE` klauzuli hello `PROCESS` instrukcji podstawowy skrypt hello U-SQL. Potrzebujemy toouse hello poprawne dane wpisz tekst tutaj.

Dla danych wyjściowych, użyj hello `output.Set` metody.

Ważne jest toonote tej niestandardowej producent wyświetla tylko kolumny i wartości, które są zdefiniowane z hello `output.Set` wywołania metody.

```
output.Set<string>("mycolumn", mycolumn);
```

dane wyjściowe procesora rzeczywistych Hello jest wyzwalane przez wywołanie metody `return output.AsReadOnly();`.

Poniżej przedstawiono przykład procesora:

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

W tym scenariuszu przypadek użycia procesora hello generuje nową kolumnę o nazwie "full_description" łącząc hello istniejące kolumny — w tym przypadku "użytkownika" wielkimi literami i "des". Również generuje identyfikator GUID i zwraca hello oryginalnego i nowej wartości identyfikatora GUID.

Jak widać w poprzednim przykładzie hello, należy wywołać metodę C# podczas `output.Set` wywołania metody.

Poniżej przedstawiono przykład podstawowego skryptu U-SQL, który używa niestandardowego procesora:

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

## <a name="use-user-defined-appliers"></a>Użyj appliers zdefiniowane przez użytkownika
U-SQL applier zdefiniowane przez użytkownika umożliwia funkcja tooinvoke niestandardowych C# dla każdego wiersza, który jest zwracany przez hello Tabela zewnętrzna wyrażenie zapytania. dane wejściowe Hello jest obliczane dla każdego wiersza z powitania po lewej stronie dane wejściowe i hello wierszy, które są tworzone są łączone na powitania ostateczne dane wyjściowe. Hello listy kolumn, które są tworzone przez operatora APPLY hello są kombinacją hello hello zestawu kolumn w lewo hello i hello prawo danych wejściowych.

Zdefiniowane przez użytkownika applier jest wywoływany jako część hello wybierz USQL wyrażenia.

Typowy Hello wywołania toohello użytkownika applier prawdopodobnie hello następujące:

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

Aby uzyskać więcej informacji o używaniu appliers w wyrażeniu SELECT, zobacz [U-SQL wybierz wybrać między Zastosuj i zewnętrzne](https://msdn.microsoft.com/library/azure/mt621307.aspx).

Witaj użytkownika applier klasy podstawowej definicji jest następujący:

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

toodefine applier zdefiniowane przez użytkownika, potrzebujemy toocreate hello `IApplier` interfejsu z hello [`SqlUserDefinedApplier`] atrybut, który jest opcjonalne dla definicji applier zdefiniowane przez użytkownika.

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

* Zastosuj jest wywoływana dla każdego wiersza tabeli zewnętrznej hello. Zwraca hello `IUpdatableRow` output zestawu wierszy.
* Hello Konstruktor klasy jest używane toopass parametry toohello applier zdefiniowane przez użytkownika.

**SqlUserDefinedApplier** wskazuje, czy typ hello powinny być rejestrowane jako applier zdefiniowane przez użytkownika. Ta klasa nie może być dziedziczona.

**SqlUserDefinedApplier** jest **opcjonalne** dla definicji applier zdefiniowane przez użytkownika.


Obiekty główne programowania Hello są następujące:

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

Wejściowe zestawy wierszy są przekazywane jako `IRow` wejściowego. Witaj wierszy dane wyjściowe są generowane jako `IUpdatableRow` interfejsu danych wyjściowych.

Można ustalić nazwy poszczególnych kolumn przy hello wywoływania `IRow` metody schematu.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

tooget hello rzeczywistych wartości danych z hello przychodzące `IRow`, możemy użyć metody Get() hello `IRow` interfejsu.

```
mycolumn = row.Get<int>("mycolumn")
```

Lub używamy nazwy kolumny schematu hello:

```
row.Get<int>(row.Schema[0].Name)
```

Witaj dane wyjściowe należy ustawić wartości z `IUpdatableRow` danych wyjściowych:

```
output.Set<int>("mycolumn", mycolumn)
```

Jest ważne toounderstand, że niestandardowe appliers output tylko kolumny i wartości, które są zdefiniowane z `output.Set` wywołania metody.

rzeczywiste dane wyjściowe Hello jest wyzwalane przez wywołanie metody `yield return output.AsReadOnly();`.

Hello użytkownika applier parametry mogą być przekazywane toohello konstruktora. Applier może zwracać zmienną liczbę kolumn, które wymagają toobe zdefiniowane podczas wywołania applier hello w podstawowej skryptu U-SQL.

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

Oto przykład applier użytkownika hello:

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

Hello podstawowej skryptu U-SQL dla tego użytkownika applier jest następujący:

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

W tym scenariuszem użycia, zdefiniowane przez użytkownika applier działa jako wartości rozdzielane przecinkami analizatora składni właściwości floty samochodów hello. wiersze pliku wejściowego Hello wyglądać hello następujące czynności:

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

Jest to typowe tabulacji TSV plik z kolumną właściwości zawierającego właściwości samochodu, takich jak marka i model. Te właściwości muszą być analizowany toohello kolumn tabeli. applier Hello, który został dostarczony umożliwia również toogenerate dynamiczne liczba właściwości w hello powoduje zestawu wierszy, na podstawie parametru hello, która została przekazana. Można wygenerować właściwości wszystkich lub określonych tylko właściwości.

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

Witaj applier zdefiniowane przez użytkownika można wywołać jako nowe wystąpienie obiektu applier:

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

Lub wywołanie metody fabryki otoki hello:

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a>Użyj combiners zdefiniowane przez użytkownika
Zdefiniowane przez użytkownika łączenia lub UDC, umożliwia toocombine wiersze z lewego i prawego zestawów wierszy, opartych na logice niestandardowej. Zdefiniowane przez użytkownika łączenia jest używany z łączenia wyrażenia.

Łączenia jest wywoływany z hello łączenie wyrażenie, które zawiera hello niezbędne informacje na temat zestawów wierszy zarówno hello wejściowych, grupowanie kolumn, hello hello oczekiwany wynik schematu i dodatkowe informacje.

toocall łączenia w podstawowej skryptu U-SQL, stosujemy hello następującej składni:

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

Aby uzyskać więcej informacji, zobacz [łączenia wyrażenia (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).

toodefine łączenia zdefiniowane przez użytkownika, potrzebujemy toocreate hello `ICombiner` interfejsu z hello [`SqlUserDefinedCombiner`] atrybut, który jest opcjonalne dla definicji łączenia zdefiniowane przez użytkownika.

Podstawa `ICombiner` definicji klasy:

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

Witaj niestandardowej implementacji `ICombiner` interfejsu powinny zawierać definicji hello `IEnumerable<IRow>` połączyć zastąpienie.

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

Witaj **SqlUserDefinedCombiner** atrybut wskazuje, że typ hello powinny być rejestrowane jako łączenia zdefiniowane przez użytkownika. Ta klasa nie może być dziedziczona.

**SqlUserDefinedCombiner** jest używane toodefine hello łączenia tryb właściwości. Jest opcjonalny atrybut dla definicji łączenia zdefiniowane przez użytkownika.

Tryb CombinerMode

Wyliczenia CombinerMode może zająć hello następujące wartości:

* Pełny (0), każdy wiersz danych wyjściowych zależy od potencjalnie wszystkie wiersze danych wejściowych powitania od lewej i prawej z hello sama wartość klucza.

* Każdy wiersz danych wyjściowych jest zależna od pojedynczy wiersz wejściowych od lewej hello lewej strony (1) (i potencjalnie wszystkie wiersze z tabeli hello prawo z hello sama wartość klucza).

* Każdy wiersz danych wyjściowych jest zależna od pojedynczy wiersz wejściowych z prawej hello prawo [2] (i potencjalnie wszystkie wiersze z tabeli po lewej hello z hello sama wartość klucza).

* Wewnętrzny (3) każdy wiersz danych wyjściowych zależy od pojedynczego danych wejściowych wiersza w lewo i prawo z hello takie same wartości.

Przykład: [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]


Obiekty główne programowania Hello są:

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

Wejściowe zestawy wierszy są przekazywane jako **po lewej stronie** i **prawo** `IRowset` typ interfejsu. Oba zestawy wierszy musi zostać wyliczone do przetwarzania. Można tylko wyliczyć każdy interfejs, dlatego firma Microsoft ma tooenumerate i jego pamięci podręcznej, jeśli to konieczne.

Na potrzeby buforowania, można utworzyć listy\<T\> typ konstrukcji pamięci w związku z tym składnika LINQ wykonywanie zapytania, w szczególności listę <`IRow`>. Typ anonimowy danych Hello może służyć podczas wyliczania również.

Zobacz [wprowadzenie tooLINQ kwerend (C#)](https://msdn.microsoft.com/library/bb397906.aspx) uzyskać więcej informacji dotyczących zapytań LINQ i [IEnumerable\<T\> interfejsu](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) Aby uzyskać więcej informacji na temat interfejsu IEnumerable\<T\> interfejsu.

tooget hello rzeczywistych wartości danych z hello przychodzące `IRowset`, możemy użyć metody Get() hello `IRow` interfejsu.

```
mycolumn = row.Get<int>("mycolumn")
```

Można ustalić nazwy poszczególnych kolumn przy hello wywoływania `IRow` metody schematu.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

Lub za pomocą nazwy kolumny schematu hello:

```
c# row.Get<int>(row.Schema[0].Name)
```

Wyliczenie ogólne Hello za pomocą LINQ wygląda hello:

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

Po wyliczania oba zestawy wierszy, zamierzamy tooloop za pośrednictwem wszystkich wierszy. Dla każdego wiersza w zestawie wierszy po lewej stronie powitania zamierzamy toofind wszystkie wiersze, które spełniają warunek hello naszych łączenia.

Witaj dane wyjściowe należy ustawić wartości z `IUpdatableRow` danych wyjściowych.

```
output.Set<int>("mycolumn", mycolumn)
```

rzeczywiste dane wyjściowe Hello jest wyzwalany przez wywołanie za`yield return output.AsReadOnly();`.

Poniżej przedstawiono przykład łączenia:

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

W tym scenariuszu przypadek użycia możemy tworzenia raportu analizy dla detalicznej hello. Celem Hello jest toofind wszystkie produkty, których koszt ponad 20 000 $ i że sprzedaży za pośrednictwem witryny sieci Web hello jest szybsza niż sprzedaży detalicznej regularne hello w danym okresie.

Oto hello podstawowy skrypt U-SQL. Możesz porównać logiki hello między sprzężenia regularnego i łączenia:

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

Zdefiniowane przez użytkownika łączenia można wywołać jako nowe wystąpienie obiektu applier hello:

```
USING new MyNameSpace.MyCombiner();
```


Lub wywołanie metody fabryki otoki hello:

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a>Użyj reduktory zdefiniowane przez użytkownika

U-SQL umożliwia toowrite reduktory niestandardowego zestawu wierszy w języku C# z wykorzystaniem strukturę rozszerzalności zdefiniowany przez użytkownika operator hello i implementowanie interfejsu IReducer.

Reduktor zdefiniowane przez użytkownika lub przez, może być niepotrzebne wierszy tooeliminate używane podczas wyodrębniania danych (Importuj). Jego również używane toomanipulate i ocenić, wierszy i kolumn. Opartych na logice programowania, jego można również zdefiniować wiersze, które wymagają toobe wyodrębnione.

toodefine przez klasę, potrzebujemy toocreate `IReducer` interfejsu z opcjonalną `SqlUserDefinedReducer` atrybutu.

Ten interfejs klasy powinny zawierać definicji hello `IEnumerable` zastąpienie interfejsu zestawu wierszy.

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

Witaj **SqlUserDefinedReducer** atrybut wskazuje, że typ hello powinny być rejestrowane jako reduktor zdefiniowane przez użytkownika. Ta klasa nie może być dziedziczona.
**SqlUserDefinedReducer** jest opcjonalny atrybut dla definicji reduktor zdefiniowane przez użytkownika. Został on użyty toodefine IsRecursive właściwości.

* wartość logiczna IsRecursive    
* **wartość true,** = wskazuje, czy ta reduktor jest idempotentności

Obiekty główne programowania Hello są **wejściowych** i **dane wyjściowe**. obiekt wejściowy Hello jest używane tooenumerate wiersze danych wejściowych. Dane wyjściowe są używane tooset wiersze danych wyjściowych wyniku zmniejszenie działania.

Wyliczenia wiersze danych wejściowych używamy hello `Row.Get` metody.

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

Witaj parametr hello `Row.Get` kolumny, która jest przekazywany jako część hello jest metoda `PRODUCE` klasy hello `REDUCE` instrukcji podstawowy skrypt hello U-SQL. Potrzebujemy toouse hello poprawne dane w tym miejscu wpisz również.

Dla danych wyjściowych, użyj hello `output.Set` metody.

Jest ważne toounderstand, który hello niestandardowych reduktor tylko dane wyjściowe wartości, które są zdefiniowane z `output.Set` wywołania metody.

```
output.Set<string>("mycolumn", guid);
```

dane wyjściowe rzeczywiste reduktor Hello jest wyzwalane przez wywołanie metody `yield return output.AsReadOnly();`.

Poniżej przedstawiono przykład reduktor:

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

W tym scenariuszu przypadek użycia reduktor hello pomija wiersze z Pusta nazwa użytkownika. Dla każdego wiersza w zestawie wierszy go odczytuje każdej wymaganej kolumny, a następnie oblicza długość hello hello nazwy użytkownika. Rzeczywiste wiersza hello go generuje tylko wtedy, gdy długość wartości nazwy użytkownika jest większa niż 0.

Poniżej przedstawiono podstawowy skryptu U-SQL, który używa niestandardowych reduktor:

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
