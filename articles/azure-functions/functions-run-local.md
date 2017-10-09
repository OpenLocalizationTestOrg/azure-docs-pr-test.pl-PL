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
# <a name="code-and-test-azure-functions-locally"></a><span data-ttu-id="6d61e-103">Kodu i przetestuj usługę Azure functions lokalnie</span><span class="sxs-lookup"><span data-stu-id="6d61e-103">Code and test Azure functions locally</span></span>

<span data-ttu-id="6d61e-104">Podczas hello [portalu Azure] zapewnia pełny zestaw narzędzi do tworzenia i testowania usługi Azure Functions, wielu deweloperów preferowane środowisko rozwoju lokalnego.</span><span class="sxs-lookup"><span data-stu-id="6d61e-104">While hello [Azure portal] provides a full set of tools for developing and testing Azure Functions, many developers prefer a local development experience.</span></span> <span data-ttu-id="6d61e-105">Środowisko Azure Functions umożliwia łatwe toouse Ulubione edytora i rozwoju lokalnego narzędzia toodevelop kodu i testowania funkcji na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="6d61e-105">Azure Functions makes it easy toouse your favorite code editor and local development tools toodevelop and test your functions on your local computer.</span></span> <span data-ttu-id="6d61e-106">Funkcji mogą wyzwalać zdarzeń na platformie Azure, a Twoje C# i funkcji JavaScript można debugować na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="6d61e-106">Your functions can trigger on events in Azure, and you can debug your C# and JavaScript functions on your local computer.</span></span> 

<span data-ttu-id="6d61e-107">Jeśli program Visual Studio C# dewelopera usługi Azure Functions także są [integruje się z programem Visual Studio 2017](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="6d61e-107">If you are a Visual Studio C# developer, Azure Functions also [integrates with Visual Studio 2017](functions-develop-vs.md).</span></span>

## <a name="install-hello-azure-functions-core-tools"></a><span data-ttu-id="6d61e-108">Zainstaluj hello Azure funkcje podstawowe narzędzia</span><span class="sxs-lookup"><span data-stu-id="6d61e-108">Install hello Azure Functions Core Tools</span></span>

<span data-ttu-id="6d61e-109">Azure funkcje podstawowe narzędzia jest lokalna wersja środowiska uruchomieniowego usługi Azure Functions hello, który można uruchomić na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="6d61e-109">Azure Functions Core Tools is a local version of hello Azure Functions runtime that you can run on your local Windows computer.</span></span> <span data-ttu-id="6d61e-110">Nie jest emulatorem ani symulatorem.</span><span class="sxs-lookup"><span data-stu-id="6d61e-110">It's not an emulator or simulator.</span></span> <span data-ttu-id="6d61e-111">Ma ona hello tego samego środowiska uruchomieniowego tej funkcji na platformie Azure uprawnień.</span><span class="sxs-lookup"><span data-stu-id="6d61e-111">It's hello same runtime that powers Functions in Azure.</span></span>

<span data-ttu-id="6d61e-112">Witaj [Azure funkcje podstawowe narzędzia] podano jako pakietu npm.</span><span class="sxs-lookup"><span data-stu-id="6d61e-112">hello [Azure Functions Core Tools] is provided as an npm package.</span></span> <span data-ttu-id="6d61e-113">Należy najpierw [zainstalować NodeJS](https://docs.npmjs.com/getting-started/installing-node), która obejmuje npm.</span><span class="sxs-lookup"><span data-stu-id="6d61e-113">You must first [install NodeJS](https://docs.npmjs.com/getting-started/installing-node), which includes npm.</span></span>  

>[!NOTE]
><span data-ttu-id="6d61e-114">W tej chwili hello Azure funkcje podstawowe narzędzia pakietu można można zainstalować tylko na komputerach z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="6d61e-114">At this time, hello Azure Functions Core Tools package can only be installed on Windows computers.</span></span> <span data-ttu-id="6d61e-115">To ograniczenie jest ze względu na tymczasowe ograniczenie tooa hello funkcji hosta.</span><span class="sxs-lookup"><span data-stu-id="6d61e-115">This restriction is due tooa temporary limitation in hello Functions host.</span></span>

<span data-ttu-id="6d61e-116">[Azure funkcje podstawowe narzędzia] dodaje powitania po aliasy poleceń:</span><span class="sxs-lookup"><span data-stu-id="6d61e-116">[Azure Functions Core Tools] adds hello following command aliases:</span></span>
* <span data-ttu-id="6d61e-117">**FUNC**</span><span class="sxs-lookup"><span data-stu-id="6d61e-117">**func**</span></span>
* <span data-ttu-id="6d61e-118">**azfun**</span><span class="sxs-lookup"><span data-stu-id="6d61e-118">**azfun**</span></span>
* <span data-ttu-id="6d61e-119">**azurefunctions**</span><span class="sxs-lookup"><span data-stu-id="6d61e-119">**azurefunctions**</span></span>

<span data-ttu-id="6d61e-120">Wszystkie te aliasu można użyć zamiast `func` przedstawiono w przykładach hello w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="6d61e-120">All of these alias can be used instead of `func` shown in hello examples in this topic.</span></span>

## <a name="create-a-local-functions-project"></a><span data-ttu-id="6d61e-121">Tworzenie projektu funkcji lokalnej</span><span class="sxs-lookup"><span data-stu-id="6d61e-121">Create a local Functions project</span></span>

<span data-ttu-id="6d61e-122">Podczas uruchamiania lokalnego, projekt funkcji jest katalog, który ma hello pliki host.json i local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="6d61e-122">When running locally, a Functions project is a directory that has hello files host.json and local.settings.json.</span></span> <span data-ttu-id="6d61e-123">Ten katalog jest hello odpowiednik aplikacji funkcji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6d61e-123">This directory is hello equivalent of a function app in Azure.</span></span> <span data-ttu-id="6d61e-124">toolearn więcej informacji na temat hello struktury folderów usługi Azure Functions, zobacz hello [przewodnik dla deweloperów usługi Azure Functions](functions-reference.md#folder-structure).</span><span class="sxs-lookup"><span data-stu-id="6d61e-124">toolearn more about hello Azure Functions folder structure, see hello [Azure Functions developers guide](functions-reference.md#folder-structure).</span></span>

<span data-ttu-id="6d61e-125">W wierszu polecenia Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6d61e-125">At a command prompt, run hello following command:</span></span>

```
func init MyFunctionProj
```

<span data-ttu-id="6d61e-126">dane wyjściowe Hello wygląda hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="6d61e-126">hello output looks like hello following example:</span></span>

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

<span data-ttu-id="6d61e-127">tooopt poza Tworzenie repozytorium Git, użyj opcji hello `--no-source-control [-n]`.</span><span class="sxs-lookup"><span data-stu-id="6d61e-127">tooopt out of creating a Git repository, use hello option `--no-source-control [-n]`.</span></span>

<a name="local-settings"></a>

## <a name="local-settings-file"></a><span data-ttu-id="6d61e-128">Plik ustawień lokalnych</span><span class="sxs-lookup"><span data-stu-id="6d61e-128">Local settings file</span></span>

<span data-ttu-id="6d61e-129">local.settings.json pliku Hello przechowuje ustawienia Azure funkcje podstawowe narzędzia, parametry połączenia i ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6d61e-129">hello file local.settings.json stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="6d61e-130">Składa się z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="6d61e-130">It has hello following structure:</span></span>

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
| <span data-ttu-id="6d61e-131">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="6d61e-131">Setting</span></span>      | <span data-ttu-id="6d61e-132">Opis</span><span class="sxs-lookup"><span data-stu-id="6d61e-132">Description</span></span>                            |
| ------------ | -------------------------------------- |
| <span data-ttu-id="6d61e-133">**IsEncrypted**</span><span class="sxs-lookup"><span data-stu-id="6d61e-133">**IsEncrypted**</span></span> | <span data-ttu-id="6d61e-134">Gdy ustawiona zbyt**true**, wszystkie wartości są szyfrowane za pomocą klucza komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="6d61e-134">When set too**true**, all values are encrypted using a local machine key.</span></span> <span data-ttu-id="6d61e-135">Używane z `func settings` poleceń.</span><span class="sxs-lookup"><span data-stu-id="6d61e-135">Used with `func settings` commands.</span></span> <span data-ttu-id="6d61e-136">Wartość domyślna to **false**.</span><span class="sxs-lookup"><span data-stu-id="6d61e-136">Default value is **false**.</span></span> |
| <span data-ttu-id="6d61e-137">**Wartości**</span><span class="sxs-lookup"><span data-stu-id="6d61e-137">**Values**</span></span> | <span data-ttu-id="6d61e-138">Kolekcja ustawień aplikacji, używane podczas uruchamiania lokalnego.</span><span class="sxs-lookup"><span data-stu-id="6d61e-138">Collection of application settings used when running locally.</span></span> <span data-ttu-id="6d61e-139">Dodaj obiekt toothis ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6d61e-139">Add your application settings toothis object.</span></span>  |
| <span data-ttu-id="6d61e-140">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="6d61e-140">**AzureWebJobsStorage**</span></span> | <span data-ttu-id="6d61e-141">Ustawia hello toohello ciąg połączenia konta magazynu Azure, która jest używana wewnętrznie przez środowisko wykonawcze usługi Azure Functions hello.</span><span class="sxs-lookup"><span data-stu-id="6d61e-141">Sets hello connection string toohello Azure Storage account that is used internally by hello Azure Functions runtime.</span></span> <span data-ttu-id="6d61e-142">Konto magazynu Hello obsługuje swoją funkcję wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="6d61e-142">hello storage account supports your function's triggers.</span></span> <span data-ttu-id="6d61e-143">To ustawienie połączenia konta magazynu jest wymagane dla wszystkich funkcji, z wyjątkiem funkcji HTTP wyzwolone.</span><span class="sxs-lookup"><span data-stu-id="6d61e-143">This storage account connection setting is required for all functions except for HTTP triggered functions.</span></span>  |
| <span data-ttu-id="6d61e-144">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="6d61e-144">**AzureWebJobsDashboard**</span></span> | <span data-ttu-id="6d61e-145">Ustawia hello połączenia ciąg toohello usługi Azure Storage konta, które jest używane toostore hello funkcja dzienniki.</span><span class="sxs-lookup"><span data-stu-id="6d61e-145">Sets hello connection string toohello Azure Storage account that is used toostore hello function logs.</span></span> <span data-ttu-id="6d61e-146">Ta opcjonalna wartość sprawia, że dzienniki hello jest dostępne w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="6d61e-146">This optional value makes hello logs accessible in hello portal.</span></span>|
| <span data-ttu-id="6d61e-147">**Host**</span><span class="sxs-lookup"><span data-stu-id="6d61e-147">**Host**</span></span> | <span data-ttu-id="6d61e-148">Ustawienia w tej sekcji dostosować procesu hosta funkcji hello podczas uruchamiania lokalnego.</span><span class="sxs-lookup"><span data-stu-id="6d61e-148">Settings in this section customize hello Functions host process when running locally.</span></span> | 
| <span data-ttu-id="6d61e-149">**LocalHttpPort**</span><span class="sxs-lookup"><span data-stu-id="6d61e-149">**LocalHttpPort**</span></span> | <span data-ttu-id="6d61e-150">Ustawia hello domyślny port używany podczas uruchamiania lokalnego hosta funkcji hello (`func host start` i `func run`).</span><span class="sxs-lookup"><span data-stu-id="6d61e-150">Sets hello default port used when running hello local Functions host (`func host start` and `func run`).</span></span> <span data-ttu-id="6d61e-151">Witaj `--port` opcji wiersza polecenia mają pierwszeństwo przed tej wartości.</span><span class="sxs-lookup"><span data-stu-id="6d61e-151">hello `--port` command-line option takes precedence over this value.</span></span> |
| <span data-ttu-id="6d61e-152">**CORS**</span><span class="sxs-lookup"><span data-stu-id="6d61e-152">**CORS**</span></span> | <span data-ttu-id="6d61e-153">Definiuje dozwolone w przypadku źródeł hello [współużytkowanie zasobów między źródłami (CORS) do udostępniania](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span><span class="sxs-lookup"><span data-stu-id="6d61e-153">Defines hello origins allowed for [cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span> <span data-ttu-id="6d61e-154">Źródła są określane jako listę rozdzielaną przecinkami, nie może zawierać spacji.</span><span class="sxs-lookup"><span data-stu-id="6d61e-154">Origins are supplied as a comma-separated list with no spaces.</span></span> <span data-ttu-id="6d61e-155">Witaj wartość symbolu wieloznacznego (**\***) jest obsługiwana, która zezwala na żądania pochodzące z dowolnego źródła.</span><span class="sxs-lookup"><span data-stu-id="6d61e-155">hello wildcard value (**\***) is supported, which allows requests from any origin.</span></span> |
| <span data-ttu-id="6d61e-156">**ConnectionStrings**</span><span class="sxs-lookup"><span data-stu-id="6d61e-156">**ConnectionStrings**</span></span> | <span data-ttu-id="6d61e-157">Zawiera hello parametry połączenia bazy danych dla funkcji.</span><span class="sxs-lookup"><span data-stu-id="6d61e-157">Contains hello database connection strings for your functions.</span></span> <span data-ttu-id="6d61e-158">Parametry połączenia w tym obiekcie są dodawane środowiska toohello z typem dostawcy hello **System.Data.SqlClient**.</span><span class="sxs-lookup"><span data-stu-id="6d61e-158">Connection strings in this object are added toohello environment with hello provider type of **System.Data.SqlClient**.</span></span>  | 

<span data-ttu-id="6d61e-159">Większość wyzwalaczy i powiązań ma **połączenia** właściwość, która mapuje nazwę toohello ustawienie zmiennej lub aplikacji środowiska.</span><span class="sxs-lookup"><span data-stu-id="6d61e-159">Most triggers and bindings have a **Connection** property that maps toohello name of an environment variable or app setting.</span></span> <span data-ttu-id="6d61e-160">Dla każdej właściwości połączenia musi być zdefiniowana w pliku local.settings.json ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6d61e-160">For each connection property, there must be app setting defined in local.settings.json file.</span></span> 

<span data-ttu-id="6d61e-161">Te ustawienia mogą być odczytywane w kodzie jako zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="6d61e-161">These settings can also be read in your code as environment variables.</span></span> <span data-ttu-id="6d61e-162">W języku C#, użyj [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) lub [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d61e-162">In C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) or [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span></span> <span data-ttu-id="6d61e-163">W języku JavaScript, użyj `process.env`.</span><span class="sxs-lookup"><span data-stu-id="6d61e-163">In JavaScript, use `process.env`.</span></span> <span data-ttu-id="6d61e-164">Ustawienia określone jako zmienna środowiskowa mają pierwszeństwo przed wartości hello local.settings.json pliku.</span><span class="sxs-lookup"><span data-stu-id="6d61e-164">Settings specified as a system environment variable take precedence over values in hello local.settings.json file.</span></span> 

<span data-ttu-id="6d61e-165">Ustawienia w pliku local.settings.json hello są używane tylko przez narzędzia funkcji podczas uruchamiania lokalnego.</span><span class="sxs-lookup"><span data-stu-id="6d61e-165">Settings in hello local.settings.json file are only used by Functions tools when running locally.</span></span> <span data-ttu-id="6d61e-166">Domyślnie te ustawienia nie są migrowane automatycznie po tooAzure opublikowanych hello projektu.</span><span class="sxs-lookup"><span data-stu-id="6d61e-166">By default, these settings are not migrated automatically when hello project is published tooAzure.</span></span> <span data-ttu-id="6d61e-167">Użyj hello `--publish-local-settings` przełącznika [po opublikowaniu](#publish) toomake się, że te ustawienia zostaną dodane toohello funkcji aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6d61e-167">Use hello `--publish-local-settings` switch [when you publish](#publish) toomake sure these settings are added toohello function app in Azure.</span></span>

<span data-ttu-id="6d61e-168">Jeśli nie parametry połączenia magazynu prawidłowy ma wartość dla **AzureWebJobsStorage**, jest wyświetlany następujący komunikat o błędzie hello:</span><span class="sxs-lookup"><span data-stu-id="6d61e-168">When no valid storage connection string is set for **AzureWebJobsStorage**, hello following error message is shown:</span></span>  

><span data-ttu-id="6d61e-169">Brak wartości dla AzureWebJobsStorage w local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="6d61e-169">Missing value for AzureWebJobsStorage in local.settings.json.</span></span> <span data-ttu-id="6d61e-170">Jest to wymagane dla wszystkich wyzwalaczy innych niż HTTP.</span><span class="sxs-lookup"><span data-stu-id="6d61e-170">This is required for all triggers other than HTTP.</span></span> <span data-ttu-id="6d61e-171">Można uruchomić "func azure functionary pobierania aplikacji ustawień <functionAppName>" lub określić parametry połączenia w local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="6d61e-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json.</span></span>
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a><span data-ttu-id="6d61e-172">Konfigurowanie ustawień aplikacji</span><span class="sxs-lookup"><span data-stu-id="6d61e-172">Configure app settings</span></span>

<span data-ttu-id="6d61e-173">tooset wartość parametrów połączenia, możesz wybrać jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="6d61e-173">tooset a value for connection strings, you can do one of hello following:</span></span>
* <span data-ttu-id="6d61e-174">Wprowadź parametry połączenia hello z [Eksploratora usługi Storage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="6d61e-174">Enter hello connection string from [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
* <span data-ttu-id="6d61e-175">Użyj jednej z hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6d61e-175">Use one of hello following commands:</span></span>

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    <span data-ttu-id="6d61e-176">Oba polecenia wymagają możesz toofirst logowania tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6d61e-176">Both commands require you toofirst sign-in tooAzure.</span></span>

## <a name="create-a-function"></a><span data-ttu-id="6d61e-177">Tworzenie funkcji</span><span class="sxs-lookup"><span data-stu-id="6d61e-177">Create a function</span></span>

<span data-ttu-id="6d61e-178">toocreate funkcję, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6d61e-178">toocreate a function, run hello following command:</span></span>

```
func new
``` 
<span data-ttu-id="6d61e-179">`func new`obsługuje hello następujące argumenty opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="6d61e-179">`func new` supports hello following optional arguments:</span></span>

| <span data-ttu-id="6d61e-180">Argument</span><span class="sxs-lookup"><span data-stu-id="6d61e-180">Argument</span></span>     | <span data-ttu-id="6d61e-181">Opis</span><span class="sxs-lookup"><span data-stu-id="6d61e-181">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | <span data-ttu-id="6d61e-182">Szablon Hello język programowania, na przykład C#, F # lub języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6d61e-182">hello template programming language, such as C#, F#, or JavaScript.</span></span> |
| **`--template -t`** | <span data-ttu-id="6d61e-183">Nazwa szablonu Hello.</span><span class="sxs-lookup"><span data-stu-id="6d61e-183">hello template name.</span></span> |
| **`--name -n`** | <span data-ttu-id="6d61e-184">Nazwa funkcji Hello.</span><span class="sxs-lookup"><span data-stu-id="6d61e-184">hello function name.</span></span> |

<span data-ttu-id="6d61e-185">Na przykład toocreate wyzwalacza JavaScript HTTP, uruchom:</span><span class="sxs-lookup"><span data-stu-id="6d61e-185">For example, toocreate a JavaScript HTTP trigger, run:</span></span>

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

<span data-ttu-id="6d61e-186">Uruchom toocreate funkcję wyzwalane kolejki:</span><span class="sxs-lookup"><span data-stu-id="6d61e-186">toocreate a queue-triggered function, run:</span></span>

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a><span data-ttu-id="6d61e-187">Lokalnie uruchamiać funkcje</span><span class="sxs-lookup"><span data-stu-id="6d61e-187">Run functions locally</span></span>

<span data-ttu-id="6d61e-188">toorun projektem funkcje hello funkcji hosta.</span><span class="sxs-lookup"><span data-stu-id="6d61e-188">toorun a Functions project, run hello Functions host.</span></span> <span data-ttu-id="6d61e-189">Hello host umożliwia Wyzwalacze dla wszystkich funkcji w projekcie hello:</span><span class="sxs-lookup"><span data-stu-id="6d61e-189">hello host enables triggers for all functions in hello project:</span></span>

```
func host start
```

<span data-ttu-id="6d61e-190">`func host start`obsługuje hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="6d61e-190">`func host start` supports hello following options:</span></span>

| <span data-ttu-id="6d61e-191">Opcja</span><span class="sxs-lookup"><span data-stu-id="6d61e-191">Option</span></span>     | <span data-ttu-id="6d61e-192">Opis</span><span class="sxs-lookup"><span data-stu-id="6d61e-192">Description</span></span>                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | <span data-ttu-id="6d61e-193">toolisten portów lokalnych Hello na.</span><span class="sxs-lookup"><span data-stu-id="6d61e-193">hello local port toolisten on.</span></span> <span data-ttu-id="6d61e-194">Wartość domyślna: 7071.</span><span class="sxs-lookup"><span data-stu-id="6d61e-194">Default value: 7071.</span></span> |
| **`--debug <type>`** | <span data-ttu-id="6d61e-195">Opcje Hello są `VSCode` i `VS`.</span><span class="sxs-lookup"><span data-stu-id="6d61e-195">hello options are `VSCode` and `VS`.</span></span> |
| **`--cors`** | <span data-ttu-id="6d61e-196">Rozdzielana przecinkami lista źródeł CORS, nie może zawierać spacji.</span><span class="sxs-lookup"><span data-stu-id="6d61e-196">A comma-separated list of CORS origins, with no spaces.</span></span> |
| **`--nodeDebugPort -n`** | <span data-ttu-id="6d61e-197">port Hello hello węzła debugera toouse.</span><span class="sxs-lookup"><span data-stu-id="6d61e-197">hello port for hello node debugger toouse.</span></span> <span data-ttu-id="6d61e-198">Wartość domyślna: Wartość z launch.json lub 5858.</span><span class="sxs-lookup"><span data-stu-id="6d61e-198">Default: A value from launch.json or 5858.</span></span> |
| **`--debugLevel -d`** | <span data-ttu-id="6d61e-199">poziom śledzenia konsoli Hello (wyłączony, pełne, info, warning lub error).</span><span class="sxs-lookup"><span data-stu-id="6d61e-199">hello console trace level (off, verbose, info, warning, or error).</span></span> <span data-ttu-id="6d61e-200">Domyślne: informacji.</span><span class="sxs-lookup"><span data-stu-id="6d61e-200">Default: Info.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="6d61e-201">limit czasu Hello hello funkcje hosta uruchomić, w sekundach.</span><span class="sxs-lookup"><span data-stu-id="6d61e-201">hello time out for hello Functions host t     o start, in seconds.</span></span> <span data-ttu-id="6d61e-202">Wartość domyślna: 20 sekund.</span><span class="sxs-lookup"><span data-stu-id="6d61e-202">Default: 20 seconds.</span></span>|
| **`--useHttps`** | <span data-ttu-id="6d61e-203">Powiąż toohttps://localhost: {port} zamiast toohttp://localhost: {port}.</span><span class="sxs-lookup"><span data-stu-id="6d61e-203">Bind toohttps://localhost:{port} rather than toohttp://localhost:{port}.</span></span> <span data-ttu-id="6d61e-204">Domyślnie ta opcja tworzy zaufanego certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6d61e-204">By default, this option creates a trusted certificate on your computer.</span></span>|
| **`--pause-on-error`** | <span data-ttu-id="6d61e-205">Wstrzymaj na dodatkowe dane wejściowe przed zakończeniem procesu hello.</span><span class="sxs-lookup"><span data-stu-id="6d61e-205">Pause for additional input before exiting hello process.</span></span> <span data-ttu-id="6d61e-206">Przydatne przy uruchamianiu narzędzia podstawowych funkcji platformy Azure z zintegrowane środowisko programistyczne (IDE).</span><span class="sxs-lookup"><span data-stu-id="6d61e-206">Useful when launching Azure Functions Core Tools from an integrated development environment (IDE).</span></span>|

<span data-ttu-id="6d61e-207">Po uruchomieniu hosta funkcji hello danych wyjściowych hello funkcji wyzwalanych przez URL HTTP:</span><span class="sxs-lookup"><span data-stu-id="6d61e-207">When hello Functions host starts, it outputs hello URL of HTTP-triggered functions:</span></span>

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a><span data-ttu-id="6d61e-208">Debugowanie w kodzie VS lub Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6d61e-208">Debug in VS Code or Visual Studio</span></span>

<span data-ttu-id="6d61e-209">tooattach debugera, Przekaż hello `--debug` argumentu.</span><span class="sxs-lookup"><span data-stu-id="6d61e-209">tooattach a debugger, pass hello `--debug` argument.</span></span> <span data-ttu-id="6d61e-210">toodebug funkcji JavaScript, użyj programu Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="6d61e-210">toodebug JavaScript functions, use Visual Studio Code.</span></span> <span data-ttu-id="6d61e-211">C# funkcji należy użyć programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6d61e-211">For C# functions, use Visual Studio.</span></span>

<span data-ttu-id="6d61e-212">Użyj funkcji toodebug C# `--debug vs`.</span><span class="sxs-lookup"><span data-stu-id="6d61e-212">toodebug C# functions, use `--debug vs`.</span></span> <span data-ttu-id="6d61e-213">Można również użyć [Azure funkcje programu Visual Studio 2017 narzędzia](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="6d61e-213">You can also use [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span> 

<span data-ttu-id="6d61e-214">toolaunch hello host i skonfigurować debugowanie JavaScript, uruchom:</span><span class="sxs-lookup"><span data-stu-id="6d61e-214">toolaunch hello host and set up JavaScript debugging, run:</span></span>

```
func host start --debug vscode
```

<span data-ttu-id="6d61e-215">Następnie, w programie Visual Studio Code, hello **debugowania** widok, wybierz opcję **dołączyć funkcje tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="6d61e-215">Then, in Visual Studio Code, in hello **Debug** view, select **Attach tooAzure Functions**.</span></span> <span data-ttu-id="6d61e-216">Umożliwia dołączanie punktów przerwania, Sprawdź zmienne i wykonywać krokowo kodu.</span><span class="sxs-lookup"><span data-stu-id="6d61e-216">You can attach breakpoints, inspect variables, and step through code.</span></span>

![Debugowanie JavaScript z kodem Visual Studio](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a><span data-ttu-id="6d61e-218">Przekazywanie testu danych tooa funkcji</span><span class="sxs-lookup"><span data-stu-id="6d61e-218">Passing test data tooa function</span></span>

<span data-ttu-id="6d61e-219">Można także wywoływać bezpośrednio za pomocą funkcji `func run <FunctionName>` i podaj dane wejściowe dla funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="6d61e-219">You can also invoke a function directly by using `func run <FunctionName>` and provide input data for hello function.</span></span> <span data-ttu-id="6d61e-220">To polecenie jest podobne toorunning funkcji za pomocą hello **testu** kartę w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6d61e-220">This command is similar toorunning a function using hello **Test** tab in hello Azure portal.</span></span> <span data-ttu-id="6d61e-221">To polecenie uruchamia hello całej funkcji hosta.</span><span class="sxs-lookup"><span data-stu-id="6d61e-221">This command launches hello entire Functions host.</span></span>

<span data-ttu-id="6d61e-222">`func run`obsługuje hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="6d61e-222">`func run` supports hello following options:</span></span>

| <span data-ttu-id="6d61e-223">Opcja</span><span class="sxs-lookup"><span data-stu-id="6d61e-223">Option</span></span>     | <span data-ttu-id="6d61e-224">Opis</span><span class="sxs-lookup"><span data-stu-id="6d61e-224">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | <span data-ttu-id="6d61e-225">Zawartość śródwierszową.</span><span class="sxs-lookup"><span data-stu-id="6d61e-225">Inline content.</span></span> |
| **`--debug -d`** | <span data-ttu-id="6d61e-226">Dołączanie procesu hosta toohello debugera przed uruchomieniem funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="6d61e-226">Attach a debugger toohello host process before running hello function.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="6d61e-227">Toowait czas (w sekundach) do hosta lokalnego funkcje hello jest gotowy.</span><span class="sxs-lookup"><span data-stu-id="6d61e-227">Time toowait (in seconds) until hello local Functions host is ready.</span></span>|
| **`--file -f`** | <span data-ttu-id="6d61e-228">Witaj toouse nazwę pliku jako zawartości.</span><span class="sxs-lookup"><span data-stu-id="6d61e-228">hello file name toouse as content.</span></span>|
| **`--no-interactive`** | <span data-ttu-id="6d61e-229">Nie jest wyświetlany monit o wprowadzenie danych.</span><span class="sxs-lookup"><span data-stu-id="6d61e-229">Does not prompt for input.</span></span> <span data-ttu-id="6d61e-230">Przydatne w scenariuszach automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="6d61e-230">Useful for automation scenarios.</span></span>|

<span data-ttu-id="6d61e-231">Na przykład toocall funkcji wyzwalanej przez HTTP i treści przebiegu, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6d61e-231">For example, toocall an HTTP-triggered function and pass content body, run hello following command:</span></span>

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <span data-ttu-id="6d61e-232"><a name="publish"></a>Publikowanie tooAzure</span><span class="sxs-lookup"><span data-stu-id="6d61e-232"><a name="publish"></a>Publish tooAzure</span></span>

<span data-ttu-id="6d61e-233">toopublish funkcje aplikacji funkcji tooa projektu na platformie Azure, użyj hello `publish` polecenia:</span><span class="sxs-lookup"><span data-stu-id="6d61e-233">toopublish a Functions project tooa function app in Azure, use hello `publish` command:</span></span>

```
func azure functionapp publish <FunctionAppName>
```

<span data-ttu-id="6d61e-234">Program hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="6d61e-234">You can use hello following options:</span></span>

| <span data-ttu-id="6d61e-235">Opcja</span><span class="sxs-lookup"><span data-stu-id="6d61e-235">Option</span></span>     | <span data-ttu-id="6d61e-236">Opis</span><span class="sxs-lookup"><span data-stu-id="6d61e-236">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  <span data-ttu-id="6d61e-237">Ustawienia publikowania w tooAzure local.settings.json, toooverwrite monitowania, jeśli hello ustawienie już istnieje.</span><span class="sxs-lookup"><span data-stu-id="6d61e-237">Publish settings in local.settings.json tooAzure, prompting toooverwrite if hello setting already exists.</span></span>|
| **`--overwrite-settings -y`** | <span data-ttu-id="6d61e-238">Musi być używany z `-i`.</span><span class="sxs-lookup"><span data-stu-id="6d61e-238">Must be used with `-i`.</span></span> <span data-ttu-id="6d61e-239">Zastępuje AppSettings na platformie Azure wartości lokalnej, jeśli jest inny.</span><span class="sxs-lookup"><span data-stu-id="6d61e-239">Overwrites AppSettings in Azure with local value if different.</span></span> <span data-ttu-id="6d61e-240">Domyślnie jest monitu.</span><span class="sxs-lookup"><span data-stu-id="6d61e-240">Default is prompt.</span></span>|

<span data-ttu-id="6d61e-241">Witaj `publish` polecenia przekazuje hello zawartość katalogu projektu hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="6d61e-241">hello `publish` command uploads hello contents of hello Functions project directory.</span></span> <span data-ttu-id="6d61e-242">Po usunięciu plików lokalnie hello `publish` nie powoduje usunięcia ich z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6d61e-242">If you delete files locally, hello `publish` command does not delete them from Azure.</span></span> <span data-ttu-id="6d61e-243">Możesz usunąć pliki na platformie Azure przy użyciu hello [narzędzie Kudu](functions-how-to-use-azure-function-app-settings.md#kudu) w hello [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="6d61e-243">You can delete files in Azure by using hello [Kudu tool](functions-how-to-use-azure-function-app-settings.md#kudu) in hello [Azure portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d61e-244">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6d61e-244">Next steps</span></span>

<span data-ttu-id="6d61e-245">Azure funkcje podstawowe narzędzia jest [otworzyć źródła i w usłudze GitHub](https://github.com/azure/azure-functions-cli).</span><span class="sxs-lookup"><span data-stu-id="6d61e-245">Azure Functions Core Tools is [open source and hosted on GitHub](https://github.com/azure/azure-functions-cli).</span></span>  
<span data-ttu-id="6d61e-246">toofile żądanie usterki lub funkcji [Otwórz problem GitHub](https://github.com/azure/azure-functions-cli/issues).</span><span class="sxs-lookup"><span data-stu-id="6d61e-246">toofile a bug or feature request, [open a GitHub issue](https://github.com/azure/azure-functions-cli/issues).</span></span> 

<!-- LINKS -->

[Azure funkcje podstawowe narzędzia]: https://www.npmjs.com/package/azure-functions-core-tools
[portalu Azure]: https://portal.azure.com 
