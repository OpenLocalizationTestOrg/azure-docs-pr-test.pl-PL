---
title: "Dokumentacja dla deweloperów aaaJavaScript dla usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak działa toodevelop przy użyciu języka JavaScript."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "usługa Azure Functions, funkcje, przetwarzanie zdarzeń, elementy webhook, obliczanie dynamiczne, architektura bez serwera"
ms.assetid: 45dedd78-3ff9-411f-bb4b-16d29a11384c
ms.service: functions
ms.devlang: nodejs
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: 6220b42f965b6ee2463341aaf270836623fdf7fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-javascript-developer-guide"></a>Przewodnik dewelopera usługi Azure funkcji JavaScript
> [!div class="op_single_selector"]
> * [Skryptu C#](functions-reference-csharp.md)
> * [Skrypt F #](functions-reference-fsharp.md)
> * [JavaScript](functions-reference-node.md)
> 
> 

Witaj obsługi języka JavaScript dla usługi Azure Functions umożliwia łatwe tooexport funkcję, która jest przekazywany jako `context` obiekt do komunikowania się ze środowiskiem uruchomieniowym hello i odbieranie i wysyłanie danych za pośrednictwem powiązania.

W tym artykule przyjęto, że został już przeczytany hello [dokumentacja dla deweloperów usługi Azure Functions](functions-reference.md).

## <a name="exporting-a-function"></a>Eksportowanie funkcji
Wszystkie funkcje kodu JavaScript, należy wyeksportować pojedynczy `function` za pośrednictwem `module.exports` dla środowiska uruchomieniowego hello toofind hello funkcji i uruchom go. Ta funkcja musi zawsze zawierać `context` obiektu.

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by hello arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

Powiązania `direction === "in"` są przekazywane jako argumenty funkcji, co oznacza, że można używać [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically obsługi nowych danych wejściowych (na przykład za pomocą `arguments.length` tooiterate za pośrednictwem wszystkich danych wejściowych). Ta funkcja jest wygodne tylko wyzwalacz i nie dodatkowe dane wejściowe, ponieważ może jednoznacznie uzyskać dostęp do danych wyzwalacza bez odwołania do Twojej `context` obiektu.

argumenty Hello zawsze są przekazywane funkcji toohello w kolejności hello, w którym występują w *function.json*, nawet jeśli nie określisz ich w instrukcji eksportu. Na przykład, jeśli masz `function(context, a, b)` i zmień je za`function(context, a)`, nadal można uzyskać wartość hello `b` w kodzie funkcji, odwołując się zbyt`arguments[3]`.

Wszystkie powiązania, niezależnie od kierunku, również są przekazywane na powitania `context` obiektu (zobacz hello następującego skryptu). 

## <a name="context-object"></a>Obiekt kontekstu
używa środowiska wykonawczego Hello `context` tooand danych toopass obiektu z funkcji i toolet komunikacji ze środowiskiem uruchomieniowym hello.

Witaj obiekt kontekstu jest zawsze hello pierwszy parametr tooa funkcji i muszą być uwzględnione, ponieważ ma ona metody takie jak `context.done` i `context.log`, które są wymagane toouse hello runtime poprawnie. Można określić nazwę obiektu hello niezależnie od chcesz (na przykład `ctx` lub `c`).

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a>właściwość Context.Bindings

```
context.bindings
```
Zwraca nazwanego obiektu, który zawiera wszystkie dane wejściowe i wyjściowe. Na przykład Witaj po definicji powiązania w Twojej *function.json* pozwala korzystać z hello zawartość hello kolejki z hello `context.bindings.myInput` obiektu. 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains hello input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a>context.Done — metoda
```
context.done([err],[propertyBag])
```

Informuje o obsługi hello kodu zostało zakończone. Należy wywołać `context.done`, lub inny hello środowiska uruchomieniowego nie wie, że funkcja została ukończona wykonanie hello upłynął limit czasu. 

Witaj `context.done` metoda pozwala toopass kopii zarówno runtime toohello błąd zdefiniowany przez użytkownika, jak i właściwość zbiór właściwości, które właściwości hello na powitania zastąpione `context.bindings` obiektu.

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a>context.log — metoda  

```
context.log(message)
```
Umożliwia toowrite toohello dzienniki przesyłania strumieniowego konsoli na powitania domyślny poziom śledzenia. Na `context.log`, dodatkowe opcje rejestrowania metody są dostępne, które umożliwiają zapisać dziennik konsoli toohello na innych poziomach śledzenia:


| Metoda                 | Opis                                |
| ---------------------- | ------------------------------------------ |
| **Błąd (_komunikat_)**   | Zapisuje poziom tooerror rejestrowanie lub niższy.   |
| **Ostrzegaj (_komunikat_)**    | Zapisuje poziom toowarning rejestrowanie lub niższy. |
| **informacje o (_komunikat_)**    | Zapisuje poziom tooinfo rejestrowanie lub niższy.    |
| **pełne (_komunikat_)** | Zapisuje tooverbose poziomu rejestrowania.           |

Witaj poniższy przykład zapisuje konsoli toohello na poziomie śledzenia ostrzeżenie hello:

```javascript
context.log.warn("Something has happened."); 
```
Ustaw poziom śledzenia hello próg rejestrowania w pliku host.json hello lub ją wyłączyć.  Aby uzyskać więcej informacji na temat sposobu logowania toowrite toohello zobacz następną sekcję hello.

## <a name="binding-data-type"></a>Typ danych powiązania

toodefine typ danych hello powiązania wejściowego, użyj hello `dataType` właściwości w definicji powiązania hello. Na przykład tooread hello zawartości żądania HTTP w formacie binarnym, użyj typu hello `binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

Inne opcje `dataType` są `stream` i `string`.

## <a name="writing-trace-output-toohello-console"></a>Zapisywanie śledzenia danych wyjściowych toohello konsoli 

W przypadku funkcji, użyj hello `context.log` metody toowrite śledzenia danych wyjściowych toohello konsoli. W tym momencie nie można użyć `console.log` toowrite toohello konsoli.

Podczas wywoływania `context.log()`, wiadomości są zapisywane konsoli toohello na poziomie śledzenia domyślnego hello, co jest hello _informacji_ poziom śledzenia. Witaj następujący kod zapisuje konsoli toohello na poziomie śledzenia informacji hello:

```javascript
context.log({hello: 'world'});  
```

Witaj poprzedni kod jest równoważne toohello następującego kodu:

```javascript
context.log.info({hello: 'world'});  
```

Witaj następujący kod zapisuje konsoli toohello na poziomie błąd hello:

```javascript
context.log.error("An error has occurred.");  
```

Ponieważ _błąd_ hello śledzenia najwyższego poziomu, to śledzenia są zapisywane dane wyjściowe toohello na wszystkich poziomach śledzenia tak długo, jak rejestrowanie jest włączone.  


Wszystkie `context.log` metody obsługują hello sam format parametru obsługiwaną przez hello Node.js [metody util.format](https://nodejs.org/api/util.html#util_util_format_format). Należy wziąć pod uwagę hello następującego kodu, który zapisuje toohello konsoli za pomocą hello domyślny poziom śledzenia:

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

Możesz również hello zapisu sam kod w hello następującego formatu:

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a>Skonfiguruj hello poziom śledzenia dla konsoli rejestrowania

Funkcje pozwala zdefiniować poziom śledzenia próg hello do pisania toohello konsoli, co pozwala na łatwe toocontrol hello sposób śledzenia są zapisywane toohello konsoli z funkcji. Próg hello tooset wszystkie ślady zapisywane toohello konsoli, użyj hello `tracing.consoleLevel` właściwość w pliku host.json hello. To ustawienie dotyczy funkcji tooall w funkcji aplikacji. Witaj poniższy przykład przedstawia hello śledzenia próg tooenable pełne rejestrowanie:

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

Wartości typu **consoleLevel** odpowiada toohello nazwy hello `context.log` metody. Ustaw wszystkie śledzenia rejestrowania konsoli toohello toodisable **consoleLevel** too_off_. Aby uzyskać więcej informacji o pliku host.json hello, zobacz hello [temat referencyjny host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

## <a name="http-triggers-and-bindings"></a>HTTP wyzwalaczy i powiązań

HTTP i wyzwalaczy elementu webhook HTTP wyjściowe i powiązania Użyj żądania i odpowiedzi obiektów toorepresent hello HTTP wiadomości.  

### <a name="request-object"></a>Obiekt żądania

Witaj `request` obiekt ma hello następujące właściwości:

| Właściwość      | Opis                                                    |
| ------------- | -------------------------------------------------------------- |
| _treści_        | Obiekt, który zawiera hello treści żądania hello.               |
| _nagłówki_     | Obiekt, który zawiera hello nagłówki żądania.                   |
| _— Metoda_      | Metoda HTTP żądania hello Hello.                                |
| _originalUrl_ | adres URL Hello hello żądania.                                        |
| _Parametry_      | Obiekt zawierający parametry routingu hello hello żądania. |
| _zapytania_       | Obiekt zawierający parametry zapytania hello.                  |
| _rawBody_     | Witaj treść wiadomości powitania jako ciąg.                           |


### <a name="response-object"></a>Obiekt odpowiedzi

Witaj `response` obiekt ma hello następujące właściwości:

| Właściwość  | Opis                                               |
| --------- | --------------------------------------------------------- |
| _treści_    | Obiekt, który zawiera treść hello hello odpowiedzi.         |
| _nagłówki_ | Obiekt, który zawiera nagłówki odpowiedzi hello.             |
| _isRaw_   | Wskazuje, że formatowanie zostało pominięte dla hello odpowiedzi.    |
| _Stan_  | Kod stanu HTTP odpowiedzi hello Hello.                     |

### <a name="accessing-hello-request-and-response"></a>Uzyskiwanie dostępu do hello żądań i odpowiedzi 

Podczas pracy z wyzwalaczy HTTP, aby dostęp do hello obiektów żądań i odpowiedzi HTTP w dowolnej z trzech sposobów:

+ Z hello o nazwie danych wejściowych i wyjściowych powiązania. W ten sposób hello wyzwalacza HTTP i powiązania pracy hello takie same jak wszelkie inne powiązania. Witaj poniższy przykład przedstawia hello obiekt odpowiedzi przy użyciu nazwane `response` powiązania: 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ Z `req` i `res` właściwości na powitania `context` obiektu. W ten sposób można użyć hello wzorca z konwencjonalnej tooaccess HTTP danych z obiektu kontekstu hello, zamiast pełnej hello toouse `context.bindings.name` wzorca. powitania po przykładzie pokazano, jak tooaccess hello `req` i `res` obiektów na powitania `context`:

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ Wywołując `context.done()`. Specjalny rodzaj powiązanie HTTP zwraca odpowiedź hello, który jest przekazywany toohello `context.done()` metody. powitania po HTTP output definiuje powiązanie `$return` parametru wyjściowego:

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    To powiązanie danych wyjściowych oczekuje odpowiedź hello toosupply podczas wywoływania `done()`w następujący sposób:

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a>Wersja węzła i zarządzania pakietami
Wersja węzła Hello jest obecnie zablokowana na `6.5.0`. Firma Microsoft badanie włączenie obsługi więcej wersji i co można skonfigurować.

Witaj, wykonaj czynności pozwalają na wybranie pakietów w aplikacji funkcji: 

1. Przejdź do zbyt`https://<function_app_name>.scm.azurewebsites.net`.

2. Kliknij przycisk **Konsola debugowania** > **CMD**.

3. Go za`D:\home\site\wwwroot`, a następnie przeciągnij z toohello pliku package.json **wwwroot** folderu w górnej połowie hello hello strony.  
    Możesz również przekazać pliki tooyour funkcji aplikacji w inny sposób. Aby uzyskać więcej informacji, zobacz [jak tooupdate funkcji pliki aplikacji](functions-reference.md#fileupdate). 

4. Po przekazaniu pliku package.json hello Uruchom hello `npm install` w hello **konsoli zdalne wykonywanie kodu Kudu**.  
    Ta akcja spowoduje pobranie pakietów hello określonej w pliku package.json hello i ponownego uruchomienia hello funkcji aplikacji.

Po hello pakiety potrzebne są zainstalowane, podczas ich importu funkcji tooyour przez wywołanie metody `require('packagename')`w hello poniższy przykład:

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

Należy zdefiniować `package.json` pliku w katalogu głównym hello aplikacji funkcji. Definiowanie pliku hello umożliwia wszystkich funkcji w udostępnionej aplikacji hello hello same pakiety w pamięci podręcznej, co daje hello najlepszą wydajność. Jeśli wystąpi konflikt wersji, można rozwiązać go przez dodanie `package.json` plik w folderze hello określonych funkcji.  

## <a name="environment-variables"></a>Zmienne środowiskowe
tooget zmienną środowiskową lub wartość ustawienia aplikacji, użyj `process.env`, jak pokazano w hello poniższy przykład kodu:

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    context.log('Node.js timer trigger function ran!', timeStamp);   
    context.log(GetEnvironmentVariable("AzureWebJobsStorage"));
    context.log(GetEnvironmentVariable("WEBSITE_SITE_NAME"));

    context.done();
};

function GetEnvironmentVariable(name)
{
    return name + ": " + process.env[name];
}
```
## <a name="considerations-for-javascript-functions"></a>Zagadnienia dotyczące funkcji JavaScript

Podczas pracy z funkcji JavaScript, należy pamiętać o kwestiach hello w hello następujące dwie sekcje.

### <a name="choose-single-core-app-service-plans"></a>Wybierz jednordzeniowy planów usługi aplikacji

Podczas tworzenia aplikacji funkcji, który używa hello planu usługi aplikacji zaleca się wybranie planu jednordzeniowy zamiast planu z wieloma rdzeniami. Obecnie funkcji uruchamia funkcji JavaScript wydajniej na maszynach wirtualnych jednordzeniowy i przy użyciu większe maszyny wirtualne nie tworzy hello oczekiwano ulepszenia wydajności. Jeśli to konieczne, można ręcznie skalować w poziomie przez dodanie więcej wystąpień maszyny Wirtualnej jednordzeniowy, lub można włączyć automatycznego skalowania. Aby uzyskać więcej informacji, zobacz [skalowanie liczby wystąpień ręcznie lub automatycznie](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).    

### <a name="typescript-and-coffeescript-support"></a>Obsługa języka typeScript i CoffeeScript
Ponieważ wsparcia bezpośredniego jeszcze nie istnieje maszynie lub CoffeeScript kompilowanie automatycznie za pomocą środowiska uruchomieniowego hello, wsparcie takie musi toobe obsługiwane poza hello środowiska uruchomieniowego, w czasie wdrażania. 

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji zobacz następujące zasoby hello:

* [Najlepsze rozwiązania dotyczące usługi Azure Functions](functions-best-practices.md)
* [Dokumentacja usługi Azure Functions dla deweloperów](functions-reference.md)
* [Azure dokumentacja dla deweloperów funkcje C#](functions-reference-csharp.md)
* [Azure dokumentacja dla deweloperów funkcje F #](functions-reference-fsharp.md)
* [Azure funkcje wyzwalaczy i powiązań](functions-triggers-bindings.md)

