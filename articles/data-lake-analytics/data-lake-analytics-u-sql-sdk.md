---
title: "aaaScale U-SQL lokalne uruchamianie i testowanie z zestawem SDK usługi Azure Data Lake U-SQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse zestawu SDK usługi Azure Data Lake U-SQL tooscale U-SQL zadania lokalne uruchamianie i testowanie z wiersza polecenia i interfejsów programowania na na lokalnej stacji roboczej."
services: data-lake-analytics
documentationcenter: 
author: 
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: yanacai
ms.openlocfilehash: 2b0a16229789268e333f723ff6fc2c3efdc29905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a>Uruchamiania lokalnego skryptu U-SQL skali i testowania przy użyciu zestawu SDK usługi Azure Data Lake U-SQL

Podczas tworzenia skryptu U-SQL, jest typowe toorun i skrypt testu U-SQL lokalnie przed przesłać toocloud. Azure Data Lake umożliwia pakietu Nuget o nazwie zestawu SDK usługi Azure Data Lake U-SQL, w tym scenariuszu, za pomocą którego można łatwo skalować uruchamiania lokalnego skryptu U-SQL i testowania. Możliwe jest również możliwe toointegrate U-SQL testu z kompilacji hello tooautomate systemu CI (ciągłej integracji) i testowania.

Jeśli potrzebne informacje jak toomanually lokalnego Uruchom i debugowania skryptu U-SQL z narzędzi z graficznym interfejsem użytkownika, możesz użyć usługi Azure Data Lake Tools dla programu Visual Studio, w tym. Dowiedz się więcej o [tutaj](data-lake-analytics-data-lake-tools-local-run.md).

## <a name="install-azure-data-lake-u-sql-sdk"></a>Instalacja usługi Azure Data Lake U-SQL SDK

Możesz uzyskać hello zestawu SDK usługi Azure Data Lake U-SQL [tutaj](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) na Nuget.org. I przed jej użyciem należy upewnić się, że zależności w następujący sposób toomake.

### <a name="dependencies"></a>Zależności

Witaj Data Lake U-SQL SDK wymaga hello następujące zależności:

- [Microsoft .NET Framework 4.6 lub nowszą](https://www.microsoft.com/download/details.aspx?id=17851).
- Microsoft Visual C++ 14 i zestaw Windows SDK 10.0.10240.0 lub nowszą (nazywany CppSDK w tym artykule). Istnieją dwa sposoby tooget CppSDK:

    - Zainstaluj [programu Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou). W folderze Program Files hello — na przykład C:\Program Files (x86) \Windows Kits\10\ będziesz mieć folderu \Windows Kits\10. Można również hello wersji zestawu Windows 10 SDK w \Windows Kits\10\Lib. Jeśli nie widzisz tych folderów, zainstaluj pakiet Visual Studio i można się tooselect hello zestawu Windows 10 SDK podczas instalacji hello. Jeśli masz to zainstalowane z programem Visual Studio kompilatora lokalne powitania U-SQL znajdziesz ją automatycznie.

    ![Narzędzia Data Lake Tools dla programu Visual Studio lokalnego uruchomienia systemu Windows 10 SDK](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - Zainstaluj [Data Lake Tools dla programu Visual Studio](http://aka.ms/adltoolsvs). Znajdziesz się, że pliki Visual C++ i zestaw Windows SDK w C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK opakowane hello. W takim przypadku kompilatora lokalne powitania U-SQL nie można automatycznie odnaleźć hello zależności. Należy ścieżką CppSDK hello toospecify dla niego. Możesz skopiować lokalizacji tooanother pliki hello lub użyj go jako jest.

## <a name="understand-basic-concepts"></a>Zrozumienie podstawowych pojęć

### <a name="data-root"></a>Główny danych

folder główny danych Hello dotyczy konto obliczeniowe lokalne powitania "Magazyn lokalny". To konto usługi Azure Data Lake Store równoważne toohello konto usługi Data Lake Analytics. Przełączanie tooa folder różnych głównych danych jest podobnie jak przełączanie tooa magazynu innego konta. Jeśli chcesz tooaccess często udostępnionych danych z różnych głównych danych folderów, należy użyć ścieżek bezwzględnych w skryptach. Lub Utwórz łącza symbolicznego systemu plików (na przykład **mklink** na NTFS) w obszarze hello danych głównych folder toopoint toohello udostępnionych danych.

folder główny danych Hello jest używany do:

- Przechowywania metadanych lokalnego, w tym baz danych, tabel, przechowywanymi w tabeli funkcji (funkcji Tvf) i zestawy.
- Wyszukiwanie hello danych wejściowych i wyjściowych ścieżek, które są zdefiniowane jako ścieżek względnych w języku U-SQL. Używanie ścieżek względnych umożliwia łatwiejsze toodeploy Twojego tooAzure projektów języka U-SQL.

### <a name="file-path-in-u-sql"></a>Ścieżka pliku w języku U-SQL

W skryptów U-SQL, można użyć zarówno ścieżki względnej, jak i lokalną ścieżkę bezwzględną. Ścieżka względna Hello jest ścieżka folderu względna toohello określony katalog główny danych. Zaleca się, że można użyć "/" jako hello toomake separatora ścieżki skryptów zgodny z powitania po stronie serwera. Oto kilka przykładów ścieżek względnych i ich równoważne ścieżki bezwzględnej. W tym przykładzie C:\LocalRunDataRoot jest folder główny danych hello.

|Ścieżka względna|Ścieżki bezwzględne|
|-------------|-------------|
|/ABC/DEF/Input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|ABC/DEF/Input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/ABC/DEF/Input.csv |D:\abc\def\input.csv|

### <a name="working-directory"></a>Katalog roboczy

Podczas uruchamiania lokalnego skryptu U-SQL hello, przejdź do katalogu roboczego został utworzony podczas kompilacji w bieżącym katalogu uruchamiania. Ponadto danych wyjściowych kompilacji toohello, hello wymagane pliki środowiska uruchomieniowego dla lokalnych wykonań będzie katalog roboczy toothis skopiowane w tle. katalog główny folder roboczy Hello jest nazywany "ScopeWorkDir" i hello pliki w katalogu roboczego hello są następujące:

|Pliku lub katalogu|Pliku lub katalogu|Pliku lub katalogu|Definicja|Opis|
|--------------|--------------|--------------|----------|-----------|
|C6A101DDCB470506| | |Ciąg skrótu wersji środowiska wykonawczego|Pliki środowiska uruchomieniowego niezbędne do wykonania lokalnej kopii w tle|
| |Script_66AE4909AA0ED06C| |Nazwa skryptu + wyznaczania wartości skrótu ciągu ścieżki skryptu|Dane wyjściowe kompilacji i wykonywanie kroku rejestrowania|
| | |\_skrypt\_.abr|Dane wyjściowe kompilatora|Plik algebraiczną|
| | |\_ScopeCodeGen\_. *|Dane wyjściowe kompilatora|Wygenerowanego kodu zarządzanego|
| | |\_ScopeCodeGenEngine\_. *|Dane wyjściowe kompilatora|Wygenerowany kod natywny|
| | |przywoływanych zestawach|Odwołanie do zestawu|Przywoływany zestaw plików|
| | |deployed_resources|Wdrażanie zasobu|Pliki zasobów wdrożenia|
| | |xxxxxxxx.xxx[1..n]\_\*. *|Dziennik wykonywania.|Dziennik wykonywania czynności|


## <a name="use-hello-sdk-from-hello-command-line"></a>Użyj hello zestawu SDK z wiersza polecenia hello

### <a name="command-line-interface-of-hello-helper-application"></a>Interfejs wiersza polecenia z aplikacją pomocniczą hello

W obszarze directory\build\runtime zestawu SDK LocalRunHelper.exe to aplikacja wiersza polecenia pomocnika hello, która zapewnia interfejsy toomost z najczęściej używanych hello lokalnego uruchomienia funkcji. Należy pamiętać, że oba hello polecenia i przełączniki argumentów hello jest rozróżniana wielkość liter. tooinvoke go:

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

Uruchom LocalRunHelper.exe bez argumentów lub hello **pomocy** przełącznika tooshow hello informacje:

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

Informacje pomocy w hello:

-  **Polecenie** zapewnia hello nazwę polecenia.  
-  **Argument wymagany** listę argumentów, które należy podać.  
-  **Opcjonalny Argument** listę argumentów, które są opcjonalne, wartościami domyślnymi.  Argumenty opcjonalne logicznych nie mają parametrów, a ich wyglądu oznaczają tootheir ujemna wartość domyślną.

### <a name="return-value-and-logging"></a>Wartość zwracana i rejestrowanie

Zwraca aplikacją pomocniczą Hello **0** w przypadku powodzenia i **-1** niepowodzenia. Domyślnie pomocnika hello wysyła wszystkie komunikaty toohello bieżącej konsoli. Jednak większość poleceń hello obsługuje hello **path_to_log_file - MessageOut** opcjonalny argument, który przekierowuje hello generuje plik dziennika tooa.

### <a name="environment-variable-configuring"></a>Konfigurowanie zmiennej środowiskowej

Uruchom wymaga głównego określone dane jako konto magazynu lokalnego, jak i zależności dla określonej ścieżki CppSDK lokalnego U-SQL. Możesz zarówno argument hello zestawu w zmiennej środowiskowej wiersza polecenia lub ustaw dla nich.

- Zestaw hello **SCOPE_CPP_SDK** zmiennej środowiskowej.

    Jeśli środowisko Microsoft Visual C++ i zestawu SDK systemu Windows hello przez zainstalowanie narzędzi Data Lake Tools dla programu Visual Studio, sprawdź, czy hello następującego folderu:

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    Zdefiniuj nową zmienną środowiskową o nazwie **SCOPE_CPP_SDK** toopoint toothis katalogu. Lub skopiuj toohello folderu hello z innej lokalizacji i określ **SCOPE_CPP_SDK** jak.

    W zmiennej środowiskowej hello toosetting dodanie, można określić hello **- CppSDK** argumentu podczas korzystania z wiersza polecenia hello. Ten argument jest zastąpienie zmiennej środowiskowej CppSDK Twojego domyślne.

- Zestaw hello **LOCALRUN_DATAROOT** zmiennej środowiskowej.

    Zdefiniuj nową zmienną środowiskową o nazwie **LOCALRUN_DATAROOT** wskazującego toohello danych głównych.

    W zmiennej środowiskowej hello toosetting dodanie, można określić hello **- DataRoot** argumentu ze ścieżką katalogu głównym danych hello podczas korzystania z wiersza polecenia. Ten argument zastępuje zmiennej środowiskowej katalogu głównym danych programu domyślnego. Należy tooadd ten argument wiersza polecenia tooevery, których używasz, dzięki czemu mogą zastępować zmiennej środowiskowej hello domyślnego katalogu głównym danych dla wszystkich operacji.

### <a name="sdk-command-line-usage-samples"></a>Przykłady użycia wiersza polecenia zestawu SDK

#### <a name="compile-and-run"></a>Kompilowanie i uruchamianie

Witaj **Uruchom** używane jest polecenie toocompile hello skrypt, a następnie wykonaj skompilowanych wyników. Argumenty wiersza polecenia są kombinacją od **skompilować** i **wykonania**.

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

Witaj następujące czynności są opcjonalne argumenty **Uruchom**:


|Argument|Wartość domyślna|Opis|
|--------|-------------|-----------|
|Plik CodeBehind-|False|skrypt Hello ma .cs kodzie|
|-CppSDK| |CppSDK katalogu|
|-DataRoot| Zmienna środowiskowa DataRoot|DataRoot dla przebiegu lokalnego zbyt domyślna zmiennej środowiskowej "LOCALRUN_DATAROOT"|
|-MessageOut| |Komunikaty zrzutu w pliku tooa konsoli|
|-Równoległe|1|Uruchom hello wybrany plan z hello równoległości|
|— Odwołania| |Lista zestawów odwołań tooextra ścieżki lub pliki danych w kodzie, oddzielone ";"|
|-UdoRedirect|False|Generowanie konfiguracji przekierowania zestawu Udo|
|-UseDatabase|master|Toouse bazy danych dla kodu tymczasowej zestawu rejestracji|
|-Verbose|False|Pokaż szczegółowe dane wyjściowe z środowiska wykonawczego|
|-WorkDir|Bieżący katalog|Katalog dla kompilatora użycia i dane wyjściowe|
|-RunScopeCEP|0|Toouse tryb ScopeCEP|
|-ScopeCEPTempPath|Temp|Toouse ścieżki tymczasowej do strumieniowego przesyłania danych|
|-OptFlags| |Rozdzielana przecinkami lista flagi optymalizacji|


Oto przykład:

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

Oprócz łączenie **skompilować** i **wykonania**, możesz skompilować i wykonywać hello skompilowane pliki wykonywalne niezależnie.

#### <a name="compile-a-u-sql-script"></a>Kompiluj skrypt U-SQL

Witaj **skompilować** polecenie jest tooexecutables skryptu używane toocompile U-SQL.

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

Witaj następujące czynności są opcjonalne argumenty **skompilować**:


|Argument|Opis|
|--------|-----------|
| -Plik CodeBehind [domyślna wartość 'False']|skrypt Hello ma .cs kodzie|
| -CppSDK [wartość domyślna "]|CppSDK katalogu|
| -DataRoot [wartość domyślna "DataRoot zmiennej środowiskowej"]|DataRoot dla przebiegu lokalnego zbyt domyślna zmiennej środowiskowej "LOCALRUN_DATAROOT"|
| -MessageOut [wartość domyślna "]|Komunikaty zrzutu w pliku tooa konsoli|
| -Odwołuje się do [wartość domyślna "]|Lista zestawów odwołań tooextra ścieżki lub pliki danych w kodzie, oddzielone ";"|
| -Małym [domyślną wartość 'False']|Skrócona kompilacji|
| -UdoRedirect [domyślna wartość 'False']|Generowanie konfiguracji przekierowania zestawu Udo|
| -UseDatabase [wartość domyślna 'master']|Toouse bazy danych dla kodu tymczasowej zestawu rejestracji|
| -WorkDir [wartość domyślna "Bieżący katalog"]|Katalog dla kompilatora użycia i dane wyjściowe|
| -RunScopeCEP [domyślna wartość "0"]|Toouse tryb ScopeCEP|
| -ScopeCEPTempPath [wartość domyślna "temp"]|Toouse ścieżki tymczasowej do strumieniowego przesyłania danych|
| -OptFlags [wartość domyślna "]|Rozdzielana przecinkami lista flagi optymalizacji|


Oto kilka przykładów użycia.

Kompiluj skrypt U-SQL:

    LocalRunHelper compile -Script d:\test\test1.usql

Kompiluj skrypt U-SQL i ustaw folder główny danych hello. Należy pamiętać, że spowoduje to zastąpienie hello ustaw dla zmiennej środowiskowej.

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

Kompiluj skrypt U-SQL i Ustaw katalog roboczy, odwołanie do zestawu i bazy danych:

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a>Wykonanie skompilowanych wyników

Witaj **wykonania** polecenia jest używane tooexecute skompilowany wyników.   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

Witaj następujące czynności są opcjonalne argumenty **wykonania**:

|Argument|Opis|
|--------|-----------|
|-DataRoot [wartość domyślna "]|Główny danych wykonywania metadanych. Domyślnie toohello **LOCALRUN_DATAROOT** zmiennej środowiskowej.|
|-MessageOut [wartość domyślna "]|Zrzut wiadomości powitania konsoli tooa pliku.|
|-Równoległe [domyślna wartość '1']|Wskaźnik toorun hello wygenerowany lokalnego wykonywania kroków za pomocą hello określony poziom równoległości.|
|-Verbose [domyślna wartość 'False']|Wskaźnik tooshow szczegółowe dane wyjściowe z środowiska wykonawczego.|

Oto przykład użycia:

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a>Witaj SDK za pomocą interfejsów programowania

interfejsy programowania Hello znajdują się w hello LocalRunHelper.exe. Można używać ich funkcji hello toointegrate hello SDK U-SQL i hello C# test framework tooscale test lokalnego skryptu U-SQL. W tym artykule będzie używać hello standard języka C# jednostki testu projektu tooshow jak toouse te interfejsy tootest skryptu U-SQL.

### <a name="step-1-create-c-unit-test-project-and-configuration"></a>Krok 1: Tworzenie projektu testu jednostki C# i konfiguracji

- Tworzenie projektu testu jednostki C# za pomocą pliku > Nowy > Projekt > Visual C# > Test > projektu testu jednostki.
- Dodaj LocalRunHelper.exe jako punkt odniesienia dla hello projektu. Witaj LocalRunHelper.exe znajduje się pod adresem \build\runtime\LocalRunHelper.exe w pakiecie Nuget.

    ![Zestaw SDK usługi Azure Data Lake U-SQL Dodaj odwołanie](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- Zestaw SDK U-SQL **tylko** środowisko obsługi x64, upewnij się, że tooset kompilacji platformy docelowej jako x64. Które można ustawić za pomocą właściwości projektu > kompilacji > platformy docelowej.

    ![Zestaw SDK usługi Azure Data Lake U-SQL skonfigurować x64 projektu](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- Upewnij się, że tooset środowiska testowego jako x64. W programie Visual Studio, możesz ustawić za pomocą testu > Testuj ustawienia > domyślny procesor > x64.

    ![Zestaw SDK usługi Azure Data Lake U-SQL skonfigurować x64 środowiska testowego](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- Upewnij się, że toocopy wszystkie pliki zależności w katalogu roboczego tooproject NugetPackage\build\runtime\, który zazwyczaj znajduje się w obszarze ProjectFolder\bin\x64\Debug.

### <a name="step-2-create-u-sql-script-test-case"></a>Krok 2: Tworzenie przypadku testowego skryptu U-SQL

Poniżej znajduje się hello przykładowy kod dla testu skryptu U-SQL. Do testowania, należy tooprepare skrypty, pliki wejściowe i oczekiwane dane wyjściowe.

    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System.IO;
    using System.Text;
    using System.Security.Cryptography;
    using Microsoft.Analytics.LocalRun;

    namespace UnitTestProject1
    {
        [TestClass]
        public class USQLUnitTest
        {
            [TestMethod]
            public void TestUSQLScript()
            {
                //Specify hello local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure hello DateRoot path, Script Path and CPPSDK path
                localrun.DataRoot = "../../../";
                localrun.ScriptPath = "../../../Script/Script.usql";
                localrun.CppSdkDir = "../../../CppSDK";

                //Run U-SQL script
                localrun.DoRun();

                //Script output 
                string Result = Path.Combine(localrun.DataRoot, "Output/result.csv");

                //Expected script output
                string ExpectedResult = "../../../ExpectedOutput/result.csv";

                Test.Helpers.FileAssert.AreEqual(Result, ExpectedResult);

                //Don't forget tooclose MessageOutput tooget logs into file
                MessageOutput.Close();
            }
        }
    }

    namespace Test.Helpers
    {
        public static class FileAssert
        {
            static string GetFileHash(string filename)
            {
                Assert.IsTrue(File.Exists(filename));

                using (var hash = new SHA1Managed())
                {
                    var clearBytes = File.ReadAllBytes(filename);
                    var hashedBytes = hash.ComputeHash(clearBytes);
                    return ConvertBytesToHex(hashedBytes);
                }
            }

            static string ConvertBytesToHex(byte[] bytes)
            {
                var sb = new StringBuilder();

                for (var i = 0; i < bytes.Length; i++)
                {
                    sb.Append(bytes[i].ToString("x"));
                }
                return sb.ToString();
            }

            public static void AreEqual(string filename1, string filename2)
            {
                string hash1 = GetFileHash(filename1);
                string hash2 = GetFileHash(filename2);

                Assert.AreEqual(hash1, hash2);
            }
        }
    }


### <a name="programming-interfaces-in-localrunhelperexe"></a>Interfejsy programowania w języku LocalRunHelper.exe

LocalRunHelper.exe zapewnia hello interfejsów dla kompilacji lokalnego skryptu U-SQL, uruchom programowania, interfejsy hello itp., są następujące.

**Konstruktor**

publiczny LocalRunHelper ([System.IO.TextWriter messageOutput = null])

|Parametr|Typ|Opis|
|---------|----|-----------|
|messageOutput|System.IO.TextWriter|komunikaty Ustaw toouse toonull konsoli|

**Właściwości**

|Właściwość|Typ|Opis|
|--------|----|-----------|
|AlgebraPath|Ciąg|Witaj ścieżki tooalgebra pliku (pliku algebraiczną jest jeden z wyników kompilacji hello)|
|CodeBehindReferences|Ciąg|Jeśli skrypt hello ma dodatkowe kodzie odwołań, określ ścieżki hello oddzielone znakiem ";"|
|CppSdkDir|Ciąg|CppSDK katalogu|
|CurrentDir|Ciąg|Bieżący katalog|
|DataRoot|Ciąg|Ścieżka katalogu głównego danych|
|DebuggerMailPath|Ciąg|Witaj ścieżki toodebugger mailslot|
|GenerateUdoRedirect|wartość logiczna|Jeśli chcemy ładowania zestawu toogenerate przekierowania zastępują konfiguracji|
|HasCodeBehind|wartość logiczna|Jeśli skrypt hello ma kodzie|
|InputDir|Ciąg|Katalog dla danych wejściowych|
|MessagePath|Ciąg|Ścieżka pliku zrzutu wiadomości|
|OutputDir|Ciąg|Katalog danych wyjściowych|
|Równoległość|int|Równoległość toorun hello algebraiczną|
|ParentPid|int|Identyfikator PID procesu hello elementu nadrzędnego, na które hello monitoruje tooexit, too0 zestaw lub tooignore ujemna|
|ResultPath|Ciąg|Ścieżka pliku zrzutu wyników|
|RuntimeDir|Ciąg|Katalogu środowiska uruchomieniowego|
|scriptPath|Ciąg|Gdzie toofind hello skryptu|
|Skrócona|wartość logiczna|Skrócona kompilacji lub nie|
|TempDir|Ciąg|Katalog tymczasowy|
|UseDataBase|Ciąg|Określ hello toouse bazy danych dla kodzie rejestracji tymczasowego zestawu głównego domyślnie|
|WorkDir|Ciąg|Preferowany katalog roboczy|


**— Metoda**

|Metoda|Opis|Zwraca|Parametr|
|------|-----------|------|---------|
|publiczny bool DoCompile()|Kompilacja skryptu hello U-SQL|Wartość true w przypadku powodzenia| |
|publiczny bool DoExec()|Wykonanie hello skompilowany wyników|Wartość true w przypadku powodzenia| |
|publiczny bool DoRun()|Uruchom skrypt U-SQL hello (kompilacji + Execute)|Wartość true w przypadku powodzenia| |
|publiczny bool IsValidRuntimeDir (ciąg ścieżki)|Sprawdź, czy hello podanej ścieżki runtime prawidłową ścieżkę|Wartość true dla prawidłowe|Witaj ścieżkę katalogu środowiska uruchomieniowego|


## <a name="faq-about-common-issue"></a>Często zadawane pytania dotyczące typowych problem

### <a name="error-1"></a>Błąd 1:
E_CSC_SYSTEM_INTERNAL: Błąd wewnętrzny! Nie można załadować pliku lub zestawu 'ScopeEngineManaged.dll' lub jednej z jego zależności. Nie można odnaleźć określonego modułu Hello.

Sprawdź, czy następujące hello:

- Upewnij się, że masz x64 środowiska. Platforma docelowa kompilacji Hello i środowiska testowego hello powinien x64, zapoznaj się zbyt**krok 1: tworzenie C# jednostki Testowanie projektu i konfiguracji** powyżej.
- Upewnij się, że zostały skopiowane wszystkie pliki zależności w katalogu roboczego tooproject NugetPackage\build\runtime\.


## <a name="next-steps"></a>Następne kroki

* toolearn U-SQL, zobacz [wprowadzenie do języka Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).
* informacje diagnostyczne toolog, zobacz [uzyskiwanie dostępu do dzienników diagnostycznych dla usługi Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).
* toosee bardziej złożonego zapytania, zobacz [analizowanie dzienników witryn sieci Web przy użyciu usługi Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).
* Zobacz szczegóły zadania tooview, [użyj przeglądarki zadania i widok zadań dla zadania usługi Azure Data Lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md).
* widoku wykonania wierzchołka hello toouse, zobacz [hello użyj widoku wykonania wierzchołka w narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).
