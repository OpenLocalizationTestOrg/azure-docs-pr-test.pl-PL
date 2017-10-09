---
title: "aaaDevelop i wykonywania Azure działa lokalnie | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocode i testowania Azure działa na komputerze lokalnym przed uruchomieniem funkcji platformy Azure."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
ms.assetid: 242736be-ec66-4114-924b-31795fd18884
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 07/12/2017
ms.author: glenga
ms.openlocfilehash: 342ed4d6df41a2d2df9067948e19e347bb52c844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="code-and-test-azure-functions-locally"></a>Kodu i przetestuj usługę Azure functions lokalnie

Podczas hello [portalu Azure] zapewnia pełny zestaw narzędzi do tworzenia i testowania usługi Azure Functions, wielu deweloperów preferowane środowisko rozwoju lokalnego. Środowisko Azure Functions umożliwia łatwe toouse Ulubione edytora i rozwoju lokalnego narzędzia toodevelop kodu i testowania funkcji na komputerze lokalnym. Funkcji mogą wyzwalać zdarzeń na platformie Azure, a Twoje C# i funkcji JavaScript można debugować na komputerze lokalnym. 

Jeśli program Visual Studio C# dewelopera usługi Azure Functions także są [integruje się z programem Visual Studio 2017](functions-develop-vs.md).

## <a name="install-hello-azure-functions-core-tools"></a>Zainstaluj hello Azure funkcje podstawowe narzędzia

Azure funkcje podstawowe narzędzia jest lokalna wersja środowiska uruchomieniowego usługi Azure Functions hello, który można uruchomić na komputerze z systemem Windows. Nie jest emulatorem ani symulatorem. Ma ona hello tego samego środowiska uruchomieniowego tej funkcji na platformie Azure uprawnień.

Witaj [Azure funkcje podstawowe narzędzia] podano jako pakietu npm. Należy najpierw [zainstalować NodeJS](https://docs.npmjs.com/getting-started/installing-node), która obejmuje npm.  

>[!NOTE]
>W tej chwili hello Azure funkcje podstawowe narzędzia pakietu można można zainstalować tylko na komputerach z systemem Windows. To ograniczenie jest ze względu na tymczasowe ograniczenie tooa hello funkcji hosta.

[Azure funkcje podstawowe narzędzia] dodaje powitania po aliasy poleceń:
* **FUNC**
* **azfun**
* **azurefunctions**

Wszystkie te aliasu można użyć zamiast `func` przedstawiono w przykładach hello w tym temacie.

## <a name="create-a-local-functions-project"></a>Tworzenie projektu funkcji lokalnej

Podczas uruchamiania lokalnego, projekt funkcji jest katalog, który ma hello pliki host.json i local.settings.json. Ten katalog jest hello odpowiednik aplikacji funkcji na platformie Azure. toolearn więcej informacji na temat hello struktury folderów usługi Azure Functions, zobacz hello [przewodnik dla deweloperów usługi Azure Functions](functions-reference.md#folder-structure).

W wierszu polecenia Uruchom następujące polecenie hello:

```
func init MyFunctionProj
```

dane wyjściowe Hello wygląda hello poniższy przykład:

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

tooopt poza Tworzenie repozytorium Git, użyj opcji hello `--no-source-control [-n]`.

<a name="local-settings"></a>

## <a name="local-settings-file"></a>Plik ustawień lokalnych

local.settings.json pliku Hello przechowuje ustawienia Azure funkcje podstawowe narzędzia, parametry połączenia i ustawień aplikacji. Składa się z następującej struktury hello:

```json
{
  "IsEncrypted": false,   
  "Values": {
    "AzureWebJobsStorage": "<connection string>", 
    "AzureWebJobsDashboard": "<connection string>", 
  },
  "Host": {
    "LocalHttpPort": 7071, 
    "CORS": "*" 
  },
  "ConnectionStrings": {
    "SQLConnectionString": "Value"
  }
}
```
| Ustawienie      | Opis                            |
| ------------ | -------------------------------------- |
| **IsEncrypted** | Gdy ustawiona zbyt**true**, wszystkie wartości są szyfrowane za pomocą klucza komputera lokalnego. Używane z `func settings` poleceń. Wartość domyślna to **false**. |
| **Wartości** | Kolekcja ustawień aplikacji, używane podczas uruchamiania lokalnego. Dodaj obiekt toothis ustawienia aplikacji.  |
| **AzureWebJobsStorage** | Ustawia hello toohello ciąg połączenia konta magazynu Azure, która jest używana wewnętrznie przez środowisko wykonawcze usługi Azure Functions hello. Konto magazynu Hello obsługuje swoją funkcję wyzwalaczy. To ustawienie połączenia konta magazynu jest wymagane dla wszystkich funkcji, z wyjątkiem funkcji HTTP wyzwolone.  |
| **AzureWebJobsDashboard** | Ustawia hello połączenia ciąg toohello usługi Azure Storage konta, które jest używane toostore hello funkcja dzienniki. Ta opcjonalna wartość sprawia, że dzienniki hello jest dostępne w portalu hello.|
| **Host** | Ustawienia w tej sekcji dostosować procesu hosta funkcji hello podczas uruchamiania lokalnego. | 
| **LocalHttpPort** | Ustawia hello domyślny port używany podczas uruchamiania lokalnego hosta funkcji hello (`func host start` i `func run`). Witaj `--port` opcji wiersza polecenia mają pierwszeństwo przed tej wartości. |
| **CORS** | Definiuje dozwolone w przypadku źródeł hello [współużytkowanie zasobów między źródłami (CORS) do udostępniania](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing). Źródła są określane jako listę rozdzielaną przecinkami, nie może zawierać spacji. Witaj wartość symbolu wieloznacznego (**\***) jest obsługiwana, która zezwala na żądania pochodzące z dowolnego źródła. |
| **ConnectionStrings** | Zawiera hello parametry połączenia bazy danych dla funkcji. Parametry połączenia w tym obiekcie są dodawane środowiska toohello z typem dostawcy hello **System.Data.SqlClient**.  | 

Większość wyzwalaczy i powiązań ma **połączenia** właściwość, która mapuje nazwę toohello ustawienie zmiennej lub aplikacji środowiska. Dla każdej właściwości połączenia musi być zdefiniowana w pliku local.settings.json ustawienia aplikacji. 

Te ustawienia mogą być odczytywane w kodzie jako zmienne środowiskowe. W języku C#, użyj [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) lub [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx). W języku JavaScript, użyj `process.env`. Ustawienia określone jako zmienna środowiskowa mają pierwszeństwo przed wartości hello local.settings.json pliku. 

Ustawienia w pliku local.settings.json hello są używane tylko przez narzędzia funkcji podczas uruchamiania lokalnego. Domyślnie te ustawienia nie są migrowane automatycznie po tooAzure opublikowanych hello projektu. Użyj hello `--publish-local-settings` przełącznika [po opublikowaniu](#publish) toomake się, że te ustawienia zostaną dodane toohello funkcji aplikacji na platformie Azure.

Jeśli nie parametry połączenia magazynu prawidłowy ma wartość dla **AzureWebJobsStorage**, jest wyświetlany następujący komunikat o błędzie hello:  

>Brak wartości dla AzureWebJobsStorage w local.settings.json. Jest to wymagane dla wszystkich wyzwalaczy innych niż HTTP. Można uruchomić "func azure functionary pobierania aplikacji ustawień <functionAppName>" lub określić parametry połączenia w local.settings.json.
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a>Konfigurowanie ustawień aplikacji

tooset wartość parametrów połączenia, możesz wybrać jedną z następujących hello:
* Wprowadź parametry połączenia hello z [Eksploratora usługi Storage Azure](http://storageexplorer.com/).
* Użyj jednej z hello następującego polecenia:

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    Oba polecenia wymagają możesz toofirst logowania tooAzure.

## <a name="create-a-function"></a>Tworzenie funkcji

toocreate funkcję, uruchom następujące polecenie hello:

```
func new
``` 
`func new`obsługuje hello następujące argumenty opcjonalne:

| Argument     | Opis                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | Szablon Hello język programowania, na przykład C#, F # lub języka JavaScript. |
| **`--template -t`** | Nazwa szablonu Hello. |
| **`--name -n`** | Nazwa funkcji Hello. |

Na przykład toocreate wyzwalacza JavaScript HTTP, uruchom:

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

Uruchom toocreate funkcję wyzwalane kolejki:

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a>Lokalnie uruchamiać funkcje

toorun projektem funkcje hello funkcji hosta. Hello host umożliwia Wyzwalacze dla wszystkich funkcji w projekcie hello:

```
func host start
```

`func host start`obsługuje hello następujące opcje:

| Opcja     | Opis                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | toolisten portów lokalnych Hello na. Wartość domyślna: 7071. |
| **`--debug <type>`** | Opcje Hello są `VSCode` i `VS`. |
| **`--cors`** | Rozdzielana przecinkami lista źródeł CORS, nie może zawierać spacji. |
| **`--nodeDebugPort -n`** | port Hello hello węzła debugera toouse. Wartość domyślna: Wartość z launch.json lub 5858. |
| **`--debugLevel -d`** | poziom śledzenia konsoli Hello (wyłączony, pełne, info, warning lub error). Domyślne: informacji.|
| **`--timeout -t`** | limit czasu Hello hello funkcje hosta uruchomić, w sekundach. Wartość domyślna: 20 sekund.|
| **`--useHttps`** | Powiąż toohttps://localhost: {port} zamiast toohttp://localhost: {port}. Domyślnie ta opcja tworzy zaufanego certyfikatu na tym komputerze.|
| **`--pause-on-error`** | Wstrzymaj na dodatkowe dane wejściowe przed zakończeniem procesu hello. Przydatne przy uruchamianiu narzędzia podstawowych funkcji platformy Azure z zintegrowane środowisko programistyczne (IDE).|

Po uruchomieniu hosta funkcji hello danych wyjściowych hello funkcji wyzwalanych przez URL HTTP:

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a>Debugowanie w kodzie VS lub Visual Studio

tooattach debugera, Przekaż hello `--debug` argumentu. toodebug funkcji JavaScript, użyj programu Visual Studio Code. C# funkcji należy użyć programu Visual Studio.

Użyj funkcji toodebug C# `--debug vs`. Można również użyć [Azure funkcje programu Visual Studio 2017 narzędzia](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/). 

toolaunch hello host i skonfigurować debugowanie JavaScript, uruchom:

```
func host start --debug vscode
```

Następnie, w programie Visual Studio Code, hello **debugowania** widok, wybierz opcję **dołączyć funkcje tooAzure**. Umożliwia dołączanie punktów przerwania, Sprawdź zmienne i wykonywać krokowo kodu.

![Debugowanie JavaScript z kodem Visual Studio](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a>Przekazywanie testu danych tooa funkcji

Można także wywoływać bezpośrednio za pomocą funkcji `func run <FunctionName>` i podaj dane wejściowe dla funkcji hello. To polecenie jest podobne toorunning funkcji za pomocą hello **testu** kartę w hello portalu Azure. To polecenie uruchamia hello całej funkcji hosta.

`func run`obsługuje hello następujące opcje:

| Opcja     | Opis                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | Zawartość śródwierszową. |
| **`--debug -d`** | Dołączanie procesu hosta toohello debugera przed uruchomieniem funkcji hello.|
| **`--timeout -t`** | Toowait czas (w sekundach) do hosta lokalnego funkcje hello jest gotowy.|
| **`--file -f`** | Witaj toouse nazwę pliku jako zawartości.|
| **`--no-interactive`** | Nie jest wyświetlany monit o wprowadzenie danych. Przydatne w scenariuszach automatyzacji.|

Na przykład toocall funkcji wyzwalanej przez HTTP i treści przebiegu, uruchom następujące polecenie hello:

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <a name="publish"></a>Publikowanie tooAzure

toopublish funkcje aplikacji funkcji tooa projektu na platformie Azure, użyj hello `publish` polecenia:

```
func azure functionapp publish <FunctionAppName>
```

Program hello następujące opcje:

| Opcja     | Opis                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  Ustawienia publikowania w tooAzure local.settings.json, toooverwrite monitowania, jeśli hello ustawienie już istnieje.|
| **`--overwrite-settings -y`** | Musi być używany z `-i`. Zastępuje AppSettings na platformie Azure wartości lokalnej, jeśli jest inny. Domyślnie jest monitu.|

Witaj `publish` polecenia przekazuje hello zawartość katalogu projektu hello funkcji. Po usunięciu plików lokalnie hello `publish` nie powoduje usunięcia ich z platformy Azure. Możesz usunąć pliki na platformie Azure przy użyciu hello [narzędzie Kudu](functions-how-to-use-azure-function-app-settings.md#kudu) w hello [portalu Azure].

## <a name="next-steps"></a>Następne kroki

Azure funkcje podstawowe narzędzia jest [otworzyć źródła i w usłudze GitHub](https://github.com/azure/azure-functions-cli).  
toofile żądanie usterki lub funkcji [Otwórz problem GitHub](https://github.com/azure/azure-functions-cli/issues). 

<!-- LINKS -->

[Azure funkcje podstawowe narzędzia]: https://www.npmjs.com/package/azure-functions-core-tools
[portalu Azure]: https://portal.azure.com 
