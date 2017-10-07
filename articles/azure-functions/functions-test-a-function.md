---
title: "aaaTesting usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Testowanie funkcji platformy Azure przy użyciu Postman, cURL i Node.js."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "Azure funkcji, funkcji, przetwarzania zdarzeń, elementów webhook, dynamiczne obliczeń, niekorzystającą architektury, testowanie"
ms.assetid: c00f3082-30d2-46b3-96ea-34faf2f15f77
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/02/2017
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a084f8dbc8089356c3c19d789dc9098f2bb63052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a>Strategie do testowania kodu w usługi Azure Functions

W tym temacie przedstawiono hello zbliża się do różnych funkcji tootest sposoby, w tym o korzystaniu z hello następujące ogólne:

+ Narzędzia oparte na protokole HTTP, takie jak cURL, Postman, a nawet przeglądarki sieci web opartych na sieci web wyzwalacze
+ Azure Eksploratora usługi Storage, tootest Wyzwalacze oparte na usłudze Azure Storage
+ Karta testu w portalu Azure Functions hello
+ Funkcja wyzwalany przez czasomierz
+ Testowanie aplikacji lub struktury

Użyj tych metod kontroli funkcja wyzwalacza HTTP, który akceptuje dane wejściowe przy użyciu jednej zapytania ciąg parametr lub hello treści żądania. W pierwszej sekcji hello tworzenia tej funkcji.

## <a name="create-a-function-for-testing"></a>Utwórz funkcję do testowania
Większość tego samouczka używamy nieco zmodyfikowaną wersję hello HttpTrigger JavaScript szablonu funkcji jest dostępna podczas tworzenia funkcji. Jeśli potrzebujesz, aby uzyskać pomoc przy tworzeniu funkcji, przejrzyj to [samouczek](functions-create-first-azure-function.md). Wybierz hello **HttpTrigger - JavaScript** szablonu podczas tworzenia funkcja testu hello w hello [portalu Azure].

Witaj domyślnego szablonu funkcji jest zasadniczo funkcji "hello world", która zwraca nazwę hello wstecz z hello żądania treści lub zapytania parametru ciągu, `name=<your name>`.  Będziemy informować kodu hello tooalso pozwalają tooprovide hello nazwy i adresu jako zawartość JSON w treści żądania hello. Następnie funkcja hello informujące o tych klienta toohello Wstecz, jeśli jest dostępna.   

Funkcja hello aktualizacji z hello następującego kodu, który zostanie wykorzystany do testowania:

```javascript
module.exports = function (context, req) {
    context.log("HTTP trigger function processed a request. RequestUri=%s", req.originalUrl);
    context.log("Request Headers = " + JSON.stringify(req.headers));
    var res;

    if (req.query.name || (req.body && req.body.name)) {
        if (typeof req.query.name != "undefined") {
            context.log("Name was provided as a query string param...");
            res = ProcessNewUserInformation(context, req.query.name);
        }
        else {
            context.log("Processing user info from request body...");
            res = ProcessNewUserInformation(context, req.body.name, req.body.address);
        }
    }
    else {
        res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done(null, res);
};
function ProcessNewUserInformation(context, name, address) {
    context.log("Processing user information...");
    context.log("name = " + name);
    var echoString = "Hello " + name;
    var res;

    if (typeof address != "undefined") {
        echoString += "\n" + "hello address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults too200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a>Testowanie funkcji z narzędzia
Poza hello portalu Azure istnieją różne narzędzia, której można tootrigger funkcji do testowania. Obejmują one testowanie narzędzia (zarówno interfejsu użytkownika i polecenia wiersza), narzędzia dostępu do usługi Azure Storage i nawet przeglądarki sieci web prostego protokołu HTTP.

### <a name="test-with-a-browser"></a>Testowanie przy użyciu przeglądarki
przeglądarki sieci web Hello jest prosty sposób tootrigger funkcje za pośrednictwem protokołu HTTP. Można użyć przeglądarki dla żądania GET, które nie wymagają ładunku treści i użyj tylko zapytania parametry.

Funkcja hello tootest zdefiniowanego wcześniej, hello kopiowania **adres Url funkcji** hello portalu. Ma hello następującej postaci:

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Dołącz hello `name` ciąg zapytania toohello parametru. Użyć rzeczywistej nazwy dla hello `<Enter a name here>` symbolu zastępczego.

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

Wklej hello URL w przeglądarce, a należy uzyskać następujące toohello podobne odpowiedzi.

![Zrzut ekranu Chrome karty przeglądarki z odpowiedzią testu](./media/functions-test-a-function/browser-test.png)

W tym przykładzie jest hello przeglądarki Chrome, która opakowuje hello zwrócony ciąg w formacie XML. Inne przeglądarki wyświetlanie tylko hello wartość ciągu.

W portalu hello **dzienniki** okno dane wyjściowe podobne następujące toohello jest rejestrowane podczas wykonywania funkcji hello:

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a>Testowanie przy Postman
Witaj zalecane narzędzie tootest Postman, która integruje się z przeglądarki Chrome hello jest większość funkcji. Zobacz tooinstall Postman, [uzyskać Postman](https://www.getpostman.com/). Postman zapewnia kontrolę nad dużo więcej atrybutów żądania HTTP.

> [!TIP]
> Narzędzie hello HTTP testowania będące najbardziej Ci. Poniżej przedstawiono niektóre tooPostman alternatyw:  
>
> * [Fiddler](http://www.telerik.com/fiddler)  
> * [Łapy](https://luckymarmot.com/paw)  
>
>

Funkcja hello tootest z treści żądania w Postman:

1. Uruchom Postman z hello **aplikacji** przycisku na powitania lewego górnego rogu okna przeglądarki Chrome.
2. Kopiowanie z **adres Url funkcji**i wklej go do Postman. Obejmuje on parametr ciągu zapytania kod dostępu hello.
3. Zmień metodę hello HTTP za**POST**.
4. Kliknij przycisk **treści** > **raw**i Dodaj podobne następujące toohello treści żądania JSON:

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. Kliknij przycisk **wysyłania**.

Witaj poniższy obraz przedstawia testowania przykład funkcja prostego echo Witaj w tym samouczku.

![Zrzut ekranu Postman interfejsu użytkownika](./media/functions-test-a-function/postman-test.png)

W portalu hello **dzienniki** okno dane wyjściowe podobne następujące toohello jest rejestrowane podczas wykonywania funkcji hello:

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a>Testowanie przy cURL z wiersza polecenia hello
Często, podczas testowania oprogramowania, nie jest konieczne toolook żadnych dalszych niż hello wiersza polecenia toohelp debugowania aplikacji. Nie różni się z testowaniem funkcje się to. Należy pamiętać, że hello cURL jest dostępny domyślnie w systemach opartych na systemie Linux. W systemie Windows, należy najpierw pobrać i zainstalować hello [narzędzie cURL](https://curl.haxx.se/).

Funkcja hello tootest czy zdefiniowanego wcześniej, hello kopiowania **adres URL funkcji** hello portalu. Ma hello następującej postaci:

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

To jest adres URL hello służącą do wyzwalania funkcji. To sprawdzić za pomocą polecenia cURL hello na powitania toomake wiersza polecenia GET (`-G` lub `--get`) żądania dotyczącego hello funkcji:

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

W tym przykładzie określonego wymaga parametru ciągu zapytania, które mogą być przekazywane jako danych (`-d`) w hello cURL polecenia:

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

Witaj wykonywania polecenia, a Zobacz hello następujące dane wyjściowe funkcji hello hello w wierszu polecenia:

![Dane wyjściowe zrzut ekranu wiersza polecenia](./media/functions-test-a-function/curl-test.png)

W portalu hello **dzienniki** okno dane wyjściowe podobne następujące toohello jest rejestrowane podczas wykonywania funkcji hello:

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a>Test wyzwalania obiektów blob przy użyciu Eksploratora usługi Storage
Funkcja wyzwalacza obiektu blob można testować przy użyciu [Eksploratora usługi Storage Azure](http://storageexplorer.com/).

1. W hello [portalu Azure] dla funkcji aplikacji, Utwórz funkcję wyzwalacza języka C#, F # lub JavaScript obiektu blob. Ustaw hello toomonitor toohello nazwę ścieżki kontenerze obiektu blob. Na przykład:

        files
2. Kliknij przycisk hello  **+**  przycisk tooselect lub utworzyć konto magazynu hello ma toouse. Następnie kliknij pozycję **Utwórz**.
3. Utwórz plik tekstowy z hello następującego tekstu i zapisz go:

        A text file for blob trigger function testing.
4. Uruchom [Eksploratora usługi Storage Azure](http://storageexplorer.com/)i połącz toohello kontenera obiektów blob na koncie magazynu hello monitorowane.
5. Kliknij przycisk **przekazać** pliku tekstowego hello tooupload.

    ![Zrzut ekranu przedstawiający Eksploratora usługi Storage](./media/functions-test-a-function/azure-storage-explorer-test.png)

Kod funkcji wyzwalacza Hello domyślnego obiektu blob raportów hello przetwarzania obiektu blob hello w dziennikach hello:

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a>Testowanie funkcji w funkcjach
Witaj portalu Azure Functions zaprojektowano toolet test HTTP oraz czasomierzem wyzwalane funkcji. Można również utworzyć tootrigger funkcje inne funkcje, które są testowania.

### <a name="test-with-hello-functions-portal-run-button"></a>Test z portalu przycisk Uruchom hello funkcji
Hello portal udostępnia **Uruchom** przycisk, w której można toodo niektóre ograniczone testowania. Dostarczyć treść żądania, używając przycisku hello, ale nie można podać parametrów ciągu zapytania lub zaktualizować nagłówki żądania.

Przetestować funkcję wyzwalacza hello HTTP utworzony wcześniej przez dodanie JSON ciąg toohello podobne, po hello **treść żądania** pola. Następnie kliknij przycisk hello **Uruchom** przycisku.

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

W portalu hello **dzienniki** okno dane wyjściowe podobne następujące toohello jest rejestrowane podczas wykonywania funkcji hello:

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a>Test z wyzwalacza bazującego na czasomierzu
Niektóre funkcje nie można przetestować odpowiednio przy użyciu narzędzi hello wspomniano powyżej. Rozważmy na przykład funkcja wyzwalacza kolejki, która jest uruchamiana, gdy komunikat jest upuścić na [magazynu kolejek Azure](../storage/queues/storage-dotnet-how-to-use-queues.md). Zawsze napisać kod toodrop wiadomości do kolejki, a na przykład w projekcie konsoli znajduje się w dalszej części tego artykułu. Istnieje jednak innej metody można użyć bezpośrednio sprawdzający funkcji.  

Można użyć wyzwalacza bazującego na czasomierzu skonfigurowane z kolejką powiązania wyjściowego. Czy kod wyzwalacza czasomierza następnie zapisywać kolejki toohello wiadomości testowej hello. W tej sekcji przedstawiono przykład.

Aby uzyskać więcej szczegółowych informacji o używaniu powiązania z usługi Azure Functions, zobacz hello [dokumentacja dla deweloperów usługi Azure Functions](functions-reference.md).

#### <a name="create-a-queue-trigger-for-testing"></a>Tworzenie kolejki wyzwalacza do testowania
toodemonstrate takie podejście, najpierw utworzymy funkcja wyzwalacza kolejki chcemy tootest kolejki o nazwie `queue-newusers`. Ta funkcja przetwarza nazwy i adresu informacji upuścić na kolejki magazynu dla nowego użytkownika.

> [!NOTE]
> Jeśli używasz innej kolejki upewnij się, należy użyć nazwy hello zgodne toohello [nazewnictwo kolejek i metadanych](https://msdn.microsoft.com/library/dd179349.aspx) reguły. W przeciwnym razie wystąpi błąd.
>
>

1. W hello [portalu Azure] dla funkcji aplikacji, kliknij przycisk **nową funkcję** > **QueueTrigger - C#**.
2. Wprowadź toobe nazwę kolejki hello monitorowane przez funkcję kolejki hello:

        queue-newusers
3. Kliknij przycisk hello  **+**  przycisk tooselect lub utworzyć konto magazynu hello ma toouse. Następnie kliknij pozycję **Utwórz**.
4. Pozostaw to okno przeglądarki w portalu otwarty, więc można monitorować hello wpisy dziennika dla kodu szablonu funkcji hello domyślne kolejki.

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a>Utwórz wiadomość w kolejce hello toodrop wyzwalacza czasomierza
1. Otwórz hello [portalu Azure] w nowym oknie przeglądarki i przejdź tooyour funkcji aplikacji.
2. Kliknij przycisk **nową funkcję** > **TimerTrigger - C#**. Wprowadź tooset wyrażenie cron częstotliwość hello kodu czasomierza testów funkcji kolejki. Następnie kliknij pozycję **Utwórz**. Jeśli chcesz toorun testu hello co 30 sekund, można użyć następujących hello [wyrażenie CRON](https://wikipedia.org/wiki/Cron#CRON_expression):

        */30 * * * * *
3. Kliknij przycisk hello **integracji** kartę nowego wyzwalacza czasomierza.
4. W obszarze **dane wyjściowe**, kliknij przycisk **+ nowe dane wyjściowe**. Następnie kliknij przycisk **kolejki** i **wybierz**.
5. Uwaga hello nazwa używana dla hello **obiekt kolejki wiadomości**. Możesz użyć tego hello czasomierza funkcja kodu.

        myQueue
6. Wprowadź nazwę kolejki hello, w którym zostanie wysłana wiadomość hello:

        queue-newusers
7. Kliknij przycisk hello  **+**  przycisk konta magazynu hello tooselect wcześniej używany z wyzwalaczem kolejki hello. Następnie kliknij przycisk **Save** (Zapisz).
8. Kliknij przycisk hello **opracowanie** kartę wyzwalacza czasomierza.
9. Witaj następującego kodu dla funkcji czasomierza hello C#, można użyć tak długo, jak używane hello kolejka sama nazwa obiektu komunikatu przedstawiona wcześniej. Następnie kliknij przycisk **Save** (Zapisz).

    ```cs
    using System;

    public static void Run(TimerInfo myTimer, out String myQueue, TraceWriter log)
    {
        String newUser =
        "{\"name\":\"User testing from C# timer function\",\"address\":\"XYZ\"}";

        log.Verbose($"C# Timer trigger function executed at: {DateTime.Now}");   
        log.Verbose($"{newUser}");   

        myQueue = newUser;
    }
    ```

W tym momencie hello funkcja czasomierza C# wykonuje co 30 sekund, jeśli użyto wyrażenia cron przykład hello. Dzienniki Hello funkcji czasomierza hello raport Każde wykonanie:

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

W oknie przeglądarki hello hello kolejki funkcji można wyświetlić każdego przetwarzanego komunikatu:

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a>Testowanie funkcji z kodu
Toocreate zewnętrznych aplikacji lub framework tootest może być konieczne funkcji.

### <a name="test-an-http-trigger-function-with-code-nodejs"></a>Testowanie funkcji wyzwalacza HTTP o kodzie: Node.js
Tooexecute aplikacji Node.js tootest żądania HTTP można użyć funkcji.
Upewnij się, że tooset:

* Witaj `host` hello żądania opcje tooyour funkcji aplikacji hosta.
* Nazwa funkcji programu hello `path`.
* Kod dostępu (`<your code>`) w hello `path`.

Przykład kodu:

```javascript
var http = require("http");

var nameQueryString = "name=Wes%20Query%20String%20Test%20From%20Node.js";

var nameBodyJSON = {
    name : "Wes testing with Node.JS code",
    address : "Dallas, T.X. 75201"
};

var bodyString = JSON.stringify(nameBodyJSON);

var options = {
  host: "functions841def78.azurewebsites.net",
  //path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9&" + nameQueryString,
  path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9",
  method: "POST",
  headers : {
      "Content-Type":"application/json",
      "Content-Length": Buffer.byteLength(bodyString)
    }    
};

callback = function(response) {
  var str = ""
  response.on("data", function (chunk) {
    str += chunk;
  });

  response.on("end", function () {
    console.log(str);
  });
}

var req = http.request(options, callback);
console.log("*** Sending name and address in body ***");
console.log(bodyString);
req.end(bodyString);
```


Dane wyjściowe:

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

W portalu hello **dzienniki** okno dane wyjściowe podobne następujące toohello jest rejestrowane podczas wykonywania funkcji hello:

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a>Testowanie funkcji wyzwalacza kolejki z kodem: C# #
Wspomniano wcześniej przetestowanie wyzwalacz kolejki przy użyciu kodu toodrop wiadomości w swojej kolejki. Witaj następującego przykładowego kodu jest oparta na powitania C# kod przedstawiony w hello [Rozpoczynanie pracy z magazynem kolejek Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) samouczka. Kod dla innych języków jest również dostępna z tego łącza.

tootest tego kodu w aplikacji konsoli, musi:

* [Konfigurowanie parametrów połączenia magazynu w pliku app.config hello](../storage/queues/storage-dotnet-how-to-use-queues.md).
* Przekaż `name` i `address` jako parametry toohello aplikacji. Na przykład `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`. (Ten kod akceptuje hello nazwę i adres dla nowego użytkownika jako argumenty wiersza polecenia w czasie wykonywania.)

Przykład C# kodu:

```cs
static void Main(string[] args)
{
    string name = null;
    string address = null;
    string queueName = "queue-newusers";
    string JSON = null;

    if (args.Length > 0)
    {
        name = args[0];
    }
    if (args.Length > 1)
    {
        address = args[1];
    }

    // Retrieve storage account from connection string
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["StorageConnectionString"]);

    // Create hello queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference tooa queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create hello queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it toohello queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message too" + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

W oknie przeglądarki hello hello kolejki funkcji można wyświetlić każdego przetwarzanego komunikatu:

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[portalu Azure]: https://portal.azure.com
