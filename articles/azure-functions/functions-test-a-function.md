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
# <a name="strategies-for-testing-your-code-in-azure-functions"></a><span data-ttu-id="67b0f-104">Strategie do testowania kodu w usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="67b0f-104">Strategies for testing your code in Azure Functions</span></span>

<span data-ttu-id="67b0f-105">W tym temacie przedstawiono hello zbliża się do różnych funkcji tootest sposoby, w tym o korzystaniu z hello następujące ogólne:</span><span class="sxs-lookup"><span data-stu-id="67b0f-105">This topic demonstrates hello various ways tootest functions, including using hello following general approaches:</span></span>

+ <span data-ttu-id="67b0f-106">Narzędzia oparte na protokole HTTP, takie jak cURL, Postman, a nawet przeglądarki sieci web opartych na sieci web wyzwalacze</span><span class="sxs-lookup"><span data-stu-id="67b0f-106">HTTP-based tools, such as cURL, Postman, and even a web browser for web-based triggers</span></span>
+ <span data-ttu-id="67b0f-107">Azure Eksploratora usługi Storage, tootest Wyzwalacze oparte na usłudze Azure Storage</span><span class="sxs-lookup"><span data-stu-id="67b0f-107">Azure Storage Explorer, tootest Azure Storage-based triggers</span></span>
+ <span data-ttu-id="67b0f-108">Karta testu w portalu Azure Functions hello</span><span class="sxs-lookup"><span data-stu-id="67b0f-108">Test tab in hello Azure Functions portal</span></span>
+ <span data-ttu-id="67b0f-109">Funkcja wyzwalany przez czasomierz</span><span class="sxs-lookup"><span data-stu-id="67b0f-109">Timer-triggered function</span></span>
+ <span data-ttu-id="67b0f-110">Testowanie aplikacji lub struktury</span><span class="sxs-lookup"><span data-stu-id="67b0f-110">Testing application or framework</span></span>

<span data-ttu-id="67b0f-111">Użyj tych metod kontroli funkcja wyzwalacza HTTP, który akceptuje dane wejściowe przy użyciu jednej zapytania ciąg parametr lub hello treści żądania.</span><span class="sxs-lookup"><span data-stu-id="67b0f-111">All these testing methods use an HTTP trigger function that accepts input through either a query string parameter or hello request body.</span></span> <span data-ttu-id="67b0f-112">W pierwszej sekcji hello tworzenia tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="67b0f-112">You create this function in hello first section.</span></span>

## <a name="create-a-function-for-testing"></a><span data-ttu-id="67b0f-113">Utwórz funkcję do testowania</span><span class="sxs-lookup"><span data-stu-id="67b0f-113">Create a function for testing</span></span>
<span data-ttu-id="67b0f-114">Większość tego samouczka używamy nieco zmodyfikowaną wersję hello HttpTrigger JavaScript szablonu funkcji jest dostępna podczas tworzenia funkcji.</span><span class="sxs-lookup"><span data-stu-id="67b0f-114">For most of this tutorial, we use a slightly modified version of hello HttpTrigger JavaScript function template that is available when you create a function.</span></span> <span data-ttu-id="67b0f-115">Jeśli potrzebujesz, aby uzyskać pomoc przy tworzeniu funkcji, przejrzyj to [samouczek](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="67b0f-115">If you need help creating a function, review this [tutorial](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="67b0f-116">Wybierz hello **HttpTrigger - JavaScript** szablonu podczas tworzenia funkcja testu hello w hello [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="67b0f-116">Choose hello **HttpTrigger- JavaScript** template when creating hello test function in hello [Azure portal].</span></span>

<span data-ttu-id="67b0f-117">Witaj domyślnego szablonu funkcji jest zasadniczo funkcji "hello world", która zwraca nazwę hello wstecz z hello żądania treści lub zapytania parametru ciągu, `name=<your name>`.</span><span class="sxs-lookup"><span data-stu-id="67b0f-117">hello default function template is basically a "hello world" function that echoes back hello name from hello request body or query string parameter, `name=<your name>`.</span></span>  <span data-ttu-id="67b0f-118">Będziemy informować kodu hello tooalso pozwalają tooprovide hello nazwy i adresu jako zawartość JSON w treści żądania hello.</span><span class="sxs-lookup"><span data-stu-id="67b0f-118">We'll update hello code tooalso allow you tooprovide hello name and an address as JSON content in hello request body.</span></span> <span data-ttu-id="67b0f-119">Następnie funkcja hello informujące o tych klienta toohello Wstecz, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="67b0f-119">Then hello function echoes these back toohello client when available.</span></span>   

<span data-ttu-id="67b0f-120">Funkcja hello aktualizacji z hello następującego kodu, który zostanie wykorzystany do testowania:</span><span class="sxs-lookup"><span data-stu-id="67b0f-120">Update hello function with hello following code, which we will use for testing:</span></span>

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

## <a name="test-a-function-with-tools"></a><span data-ttu-id="67b0f-121">Testowanie funkcji z narzędzia</span><span class="sxs-lookup"><span data-stu-id="67b0f-121">Test a function with tools</span></span>
<span data-ttu-id="67b0f-122">Poza hello portalu Azure istnieją różne narzędzia, której można tootrigger funkcji do testowania.</span><span class="sxs-lookup"><span data-stu-id="67b0f-122">Outside hello Azure portal, there are various tools that you can use tootrigger your functions for testing.</span></span> <span data-ttu-id="67b0f-123">Obejmują one testowanie narzędzia (zarówno interfejsu użytkownika i polecenia wiersza), narzędzia dostępu do usługi Azure Storage i nawet przeglądarki sieci web prostego protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="67b0f-123">These include HTTP testing tools (both UI-based and command line), Azure Storage access tools, and even a simple web browser.</span></span>

### <a name="test-with-a-browser"></a><span data-ttu-id="67b0f-124">Testowanie przy użyciu przeglądarki</span><span class="sxs-lookup"><span data-stu-id="67b0f-124">Test with a browser</span></span>
<span data-ttu-id="67b0f-125">przeglądarki sieci web Hello jest prosty sposób tootrigger funkcje za pośrednictwem protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="67b0f-125">hello web browser is a simple way tootrigger functions via HTTP.</span></span> <span data-ttu-id="67b0f-126">Można użyć przeglądarki dla żądania GET, które nie wymagają ładunku treści i użyj tylko zapytania parametry.</span><span class="sxs-lookup"><span data-stu-id="67b0f-126">You can use a browser for GET requests that do not require a body payload, and that use only query string parameters.</span></span>

<span data-ttu-id="67b0f-127">Funkcja hello tootest zdefiniowanego wcześniej, hello kopiowania **adres Url funkcji** hello portalu.</span><span class="sxs-lookup"><span data-stu-id="67b0f-127">tootest hello function we defined earlier, copy hello **Function Url** from hello portal.</span></span> <span data-ttu-id="67b0f-128">Ma hello następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="67b0f-128">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="67b0f-129">Dołącz hello `name` ciąg zapytania toohello parametru.</span><span class="sxs-lookup"><span data-stu-id="67b0f-129">Append hello `name` parameter toohello query string.</span></span> <span data-ttu-id="67b0f-130">Użyć rzeczywistej nazwy dla hello `<Enter a name here>` symbolu zastępczego.</span><span class="sxs-lookup"><span data-stu-id="67b0f-130">Use an actual name for hello `<Enter a name here>` placeholder.</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

<span data-ttu-id="67b0f-131">Wklej hello URL w przeglądarce, a należy uzyskać następujące toohello podobne odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="67b0f-131">Paste hello URL into your browser, and you should get a response similar toohello following.</span></span>

![Zrzut ekranu Chrome karty przeglądarki z odpowiedzią testu](./media/functions-test-a-function/browser-test.png)

<span data-ttu-id="67b0f-133">W tym przykładzie jest hello przeglądarki Chrome, która opakowuje hello zwrócony ciąg w formacie XML.</span><span class="sxs-lookup"><span data-stu-id="67b0f-133">This example is hello Chrome browser, which wraps hello returned string in XML.</span></span> <span data-ttu-id="67b0f-134">Inne przeglądarki wyświetlanie tylko hello wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="67b0f-134">Other browsers display just hello string value.</span></span>

<span data-ttu-id="67b0f-135">W portalu hello **dzienniki** okno dane wyjściowe podobne następujące toohello jest rejestrowane podczas wykonywania funkcji hello:</span><span class="sxs-lookup"><span data-stu-id="67b0f-135">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a><span data-ttu-id="67b0f-136">Testowanie przy Postman</span><span class="sxs-lookup"><span data-stu-id="67b0f-136">Test with Postman</span></span>
<span data-ttu-id="67b0f-137">Witaj zalecane narzędzie tootest Postman, która integruje się z przeglądarki Chrome hello jest większość funkcji.</span><span class="sxs-lookup"><span data-stu-id="67b0f-137">hello recommended tool tootest most of your functions is Postman, which integrates with hello Chrome browser.</span></span> <span data-ttu-id="67b0f-138">Zobacz tooinstall Postman, [uzyskać Postman](https://www.getpostman.com/).</span><span class="sxs-lookup"><span data-stu-id="67b0f-138">tooinstall Postman, see [Get Postman](https://www.getpostman.com/).</span></span> <span data-ttu-id="67b0f-139">Postman zapewnia kontrolę nad dużo więcej atrybutów żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="67b0f-139">Postman provides control over many more attributes of an HTTP request.</span></span>

> [!TIP]
> <span data-ttu-id="67b0f-140">Narzędzie hello HTTP testowania będące najbardziej Ci.</span><span class="sxs-lookup"><span data-stu-id="67b0f-140">Use hello HTTP testing tool that you are most comfortable with.</span></span> <span data-ttu-id="67b0f-141">Poniżej przedstawiono niektóre tooPostman alternatyw:</span><span class="sxs-lookup"><span data-stu-id="67b0f-141">Here are some alternatives tooPostman:</span></span>  
>
> * [<span data-ttu-id="67b0f-142">Fiddler</span><span class="sxs-lookup"><span data-stu-id="67b0f-142">Fiddler</span></span>](http://www.telerik.com/fiddler)  
> * [<span data-ttu-id="67b0f-143">Łapy</span><span class="sxs-lookup"><span data-stu-id="67b0f-143">Paw</span></span>](https://luckymarmot.com/paw)  
>
>

<span data-ttu-id="67b0f-144">Funkcja hello tootest z treści żądania w Postman:</span><span class="sxs-lookup"><span data-stu-id="67b0f-144">tootest hello function with a request body in Postman:</span></span>

1. <span data-ttu-id="67b0f-145">Uruchom Postman z hello **aplikacji** przycisku na powitania lewego górnego rogu okna przeglądarki Chrome.</span><span class="sxs-lookup"><span data-stu-id="67b0f-145">Start Postman from hello **Apps** button in hello upper-left corner of a Chrome browser window.</span></span>
2. <span data-ttu-id="67b0f-146">Kopiowanie z **adres Url funkcji**i wklej go do Postman.</span><span class="sxs-lookup"><span data-stu-id="67b0f-146">Copy your **Function Url**, and paste it into Postman.</span></span> <span data-ttu-id="67b0f-147">Obejmuje on parametr ciągu zapytania kod dostępu hello.</span><span class="sxs-lookup"><span data-stu-id="67b0f-147">It includes hello access code query string parameter.</span></span>
3. <span data-ttu-id="67b0f-148">Zmień metodę hello HTTP za**POST**.</span><span class="sxs-lookup"><span data-stu-id="67b0f-148">Change hello HTTP method too**POST**.</span></span>
4. <span data-ttu-id="67b0f-149">Kliknij przycisk **treści** > **raw**i Dodaj podobne następujące toohello treści żądania JSON:</span><span class="sxs-lookup"><span data-stu-id="67b0f-149">Click **Body** > **raw**, and add a JSON request body similar toohello following:</span></span>

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. <span data-ttu-id="67b0f-150">Kliknij przycisk **wysyłania**.</span><span class="sxs-lookup"><span data-stu-id="67b0f-150">Click **Send**.</span></span>

<span data-ttu-id="67b0f-151">Witaj poniższy obraz przedstawia testowania przykład funkcja prostego echo Witaj w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="67b0f-151">hello following image shows testing hello simple echo function example in this tutorial.</span></span>

![Zrzut ekranu Postman interfejsu użytkownika](./media/functions-test-a-function/postman-test.png)

<span data-ttu-id="67b0f-153">W portalu hello **dzienniki** okno dane wyjściowe podobne następujące toohello jest rejestrowane podczas wykonywania funkcji hello:</span><span class="sxs-lookup"><span data-stu-id="67b0f-153">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a><span data-ttu-id="67b0f-154">Testowanie przy cURL z wiersza polecenia hello</span><span class="sxs-lookup"><span data-stu-id="67b0f-154">Test with cURL from hello command line</span></span>
<span data-ttu-id="67b0f-155">Często, podczas testowania oprogramowania, nie jest konieczne toolook żadnych dalszych niż hello wiersza polecenia toohelp debugowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67b0f-155">Often when you're testing software, it's not necessary toolook any further than hello command line toohelp debug your application.</span></span> <span data-ttu-id="67b0f-156">Nie różni się z testowaniem funkcje się to.</span><span class="sxs-lookup"><span data-stu-id="67b0f-156">This is no different with testing functions.</span></span> <span data-ttu-id="67b0f-157">Należy pamiętać, że hello cURL jest dostępny domyślnie w systemach opartych na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="67b0f-157">Note that hello cURL is available by default on Linux-based systems.</span></span> <span data-ttu-id="67b0f-158">W systemie Windows, należy najpierw pobrać i zainstalować hello [narzędzie cURL](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="67b0f-158">On Windows, you must first download and install hello [cURL tool](https://curl.haxx.se/).</span></span>

<span data-ttu-id="67b0f-159">Funkcja hello tootest czy zdefiniowanego wcześniej, hello kopiowania **adres URL funkcji** hello portalu.</span><span class="sxs-lookup"><span data-stu-id="67b0f-159">tootest hello function that we defined earlier, copy hello **Function URL** from hello portal.</span></span> <span data-ttu-id="67b0f-160">Ma hello następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="67b0f-160">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="67b0f-161">To jest adres URL hello służącą do wyzwalania funkcji.</span><span class="sxs-lookup"><span data-stu-id="67b0f-161">This is hello URL for triggering your function.</span></span> <span data-ttu-id="67b0f-162">To sprawdzić za pomocą polecenia cURL hello na powitania toomake wiersza polecenia GET (`-G` lub `--get`) żądania dotyczącego hello funkcji:</span><span class="sxs-lookup"><span data-stu-id="67b0f-162">Test this by using hello cURL command on hello command line toomake a GET (`-G` or `--get`) request against hello function:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="67b0f-163">W tym przykładzie określonego wymaga parametru ciągu zapytania, które mogą być przekazywane jako danych (`-d`) w hello cURL polecenia:</span><span class="sxs-lookup"><span data-stu-id="67b0f-163">This particular example requires a query string parameter, which can be passed as Data (`-d`) in hello cURL command:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

<span data-ttu-id="67b0f-164">Witaj wykonywania polecenia, a Zobacz hello następujące dane wyjściowe funkcji hello hello w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="67b0f-164">Run hello command, and you see hello following output of hello function on hello command line:</span></span>

![Dane wyjściowe zrzut ekranu wiersza polecenia](./media/functions-test-a-function/curl-test.png)

<span data-ttu-id="67b0f-166">W portalu hello **dzienniki** okno dane wyjściowe podobne następujące toohello jest rejestrowane podczas wykonywania funkcji hello:</span><span class="sxs-lookup"><span data-stu-id="67b0f-166">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a><span data-ttu-id="67b0f-167">Test wyzwalania obiektów blob przy użyciu Eksploratora usługi Storage</span><span class="sxs-lookup"><span data-stu-id="67b0f-167">Test a blob trigger by using Storage Explorer</span></span>
<span data-ttu-id="67b0f-168">Funkcja wyzwalacza obiektu blob można testować przy użyciu [Eksploratora usługi Storage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="67b0f-168">You can test a blob trigger function by using [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

1. <span data-ttu-id="67b0f-169">W hello [portalu Azure] dla funkcji aplikacji, Utwórz funkcję wyzwalacza języka C#, F # lub JavaScript obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="67b0f-169">In hello [Azure portal] for your function app, create a C#, F# or JavaScript blob trigger function.</span></span> <span data-ttu-id="67b0f-170">Ustaw hello toomonitor toohello nazwę ścieżki kontenerze obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="67b0f-170">Set hello path toomonitor toohello name of your blob container.</span></span> <span data-ttu-id="67b0f-171">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="67b0f-171">For example:</span></span>

        files
2. <span data-ttu-id="67b0f-172">Kliknij przycisk hello  **+**  przycisk tooselect lub utworzyć konto magazynu hello ma toouse.</span><span class="sxs-lookup"><span data-stu-id="67b0f-172">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="67b0f-173">Następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="67b0f-173">Then click **Create**.</span></span>
3. <span data-ttu-id="67b0f-174">Utwórz plik tekstowy z hello następującego tekstu i zapisz go:</span><span class="sxs-lookup"><span data-stu-id="67b0f-174">Create a text file with hello following text, and save it:</span></span>

        A text file for blob trigger function testing.
4. <span data-ttu-id="67b0f-175">Uruchom [Eksploratora usługi Storage Azure](http://storageexplorer.com/)i połącz toohello kontenera obiektów blob na koncie magazynu hello monitorowane.</span><span class="sxs-lookup"><span data-stu-id="67b0f-175">Run [Azure Storage Explorer](http://storageexplorer.com/), and connect toohello blob container in hello storage account being monitored.</span></span>
5. <span data-ttu-id="67b0f-176">Kliknij przycisk **przekazać** pliku tekstowego hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="67b0f-176">Click **Upload** tooupload hello text file.</span></span>

    ![Zrzut ekranu przedstawiający Eksploratora usługi Storage](./media/functions-test-a-function/azure-storage-explorer-test.png)

<span data-ttu-id="67b0f-178">Kod funkcji wyzwalacza Hello domyślnego obiektu blob raportów hello przetwarzania obiektu blob hello w dziennikach hello:</span><span class="sxs-lookup"><span data-stu-id="67b0f-178">hello default blob trigger function code reports hello processing of hello blob in hello logs:</span></span>

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a><span data-ttu-id="67b0f-179">Testowanie funkcji w funkcjach</span><span class="sxs-lookup"><span data-stu-id="67b0f-179">Test a function within functions</span></span>
<span data-ttu-id="67b0f-180">Witaj portalu Azure Functions zaprojektowano toolet test HTTP oraz czasomierzem wyzwalane funkcji.</span><span class="sxs-lookup"><span data-stu-id="67b0f-180">hello Azure Functions portal is designed toolet you test HTTP and timer triggered functions.</span></span> <span data-ttu-id="67b0f-181">Można również utworzyć tootrigger funkcje inne funkcje, które są testowania.</span><span class="sxs-lookup"><span data-stu-id="67b0f-181">You can also create functions tootrigger other functions that you are testing.</span></span>

### <a name="test-with-hello-functions-portal-run-button"></a><span data-ttu-id="67b0f-182">Test z portalu przycisk Uruchom hello funkcji</span><span class="sxs-lookup"><span data-stu-id="67b0f-182">Test with hello Functions portal Run button</span></span>
<span data-ttu-id="67b0f-183">Hello portal udostępnia **Uruchom** przycisk, w której można toodo niektóre ograniczone testowania.</span><span class="sxs-lookup"><span data-stu-id="67b0f-183">hello portal provides a **Run** button that you can use toodo some limited testing.</span></span> <span data-ttu-id="67b0f-184">Dostarczyć treść żądania, używając przycisku hello, ale nie można podać parametrów ciągu zapytania lub zaktualizować nagłówki żądania.</span><span class="sxs-lookup"><span data-stu-id="67b0f-184">You can provide a request body by using hello button, but you can't provide query string parameters or update request headers.</span></span>

<span data-ttu-id="67b0f-185">Przetestować funkcję wyzwalacza hello HTTP utworzony wcześniej przez dodanie JSON ciąg toohello podobne, po hello **treść żądania** pola.</span><span class="sxs-lookup"><span data-stu-id="67b0f-185">Test hello HTTP trigger function we created earlier by adding a JSON string similar toohello following in hello **Request body** field.</span></span> <span data-ttu-id="67b0f-186">Następnie kliknij przycisk hello **Uruchom** przycisku.</span><span class="sxs-lookup"><span data-stu-id="67b0f-186">Then click hello **Run** button.</span></span>

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

<span data-ttu-id="67b0f-187">W portalu hello **dzienniki** okno dane wyjściowe podobne następujące toohello jest rejestrowane podczas wykonywania funkcji hello:</span><span class="sxs-lookup"><span data-stu-id="67b0f-187">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a><span data-ttu-id="67b0f-188">Test z wyzwalacza bazującego na czasomierzu</span><span class="sxs-lookup"><span data-stu-id="67b0f-188">Test with a timer trigger</span></span>
<span data-ttu-id="67b0f-189">Niektóre funkcje nie można przetestować odpowiednio przy użyciu narzędzi hello wspomniano powyżej.</span><span class="sxs-lookup"><span data-stu-id="67b0f-189">Some functions can't be adequately tested with hello tools mentioned previously.</span></span> <span data-ttu-id="67b0f-190">Rozważmy na przykład funkcja wyzwalacza kolejki, która jest uruchamiana, gdy komunikat jest upuścić na [magazynu kolejek Azure](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="67b0f-190">For example, consider a queue trigger function that runs when a message is dropped into [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="67b0f-191">Zawsze napisać kod toodrop wiadomości do kolejki, a na przykład w projekcie konsoli znajduje się w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="67b0f-191">You can always write code toodrop a message into your queue, and an example of this in a console project is provided later in this article.</span></span> <span data-ttu-id="67b0f-192">Istnieje jednak innej metody można użyć bezpośrednio sprawdzający funkcji.</span><span class="sxs-lookup"><span data-stu-id="67b0f-192">However, there is another approach you can use that tests functions directly.</span></span>  

<span data-ttu-id="67b0f-193">Można użyć wyzwalacza bazującego na czasomierzu skonfigurowane z kolejką powiązania wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="67b0f-193">You can use a timer trigger configured with a queue output binding.</span></span> <span data-ttu-id="67b0f-194">Czy kod wyzwalacza czasomierza następnie zapisywać kolejki toohello wiadomości testowej hello.</span><span class="sxs-lookup"><span data-stu-id="67b0f-194">That timer trigger code can then write hello test messages toohello queue.</span></span> <span data-ttu-id="67b0f-195">W tej sekcji przedstawiono przykład.</span><span class="sxs-lookup"><span data-stu-id="67b0f-195">This section walks through an example.</span></span>

<span data-ttu-id="67b0f-196">Aby uzyskać więcej szczegółowych informacji o używaniu powiązania z usługi Azure Functions, zobacz hello [dokumentacja dla deweloperów usługi Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="67b0f-196">For more in-depth information on using bindings with Azure Functions, see hello [Azure Functions developer reference](functions-reference.md).</span></span>

#### <a name="create-a-queue-trigger-for-testing"></a><span data-ttu-id="67b0f-197">Tworzenie kolejki wyzwalacza do testowania</span><span class="sxs-lookup"><span data-stu-id="67b0f-197">Create a queue trigger for testing</span></span>
<span data-ttu-id="67b0f-198">toodemonstrate takie podejście, najpierw utworzymy funkcja wyzwalacza kolejki chcemy tootest kolejki o nazwie `queue-newusers`.</span><span class="sxs-lookup"><span data-stu-id="67b0f-198">toodemonstrate this approach, we first create a queue trigger function that we want tootest for a queue named `queue-newusers`.</span></span> <span data-ttu-id="67b0f-199">Ta funkcja przetwarza nazwy i adresu informacji upuścić na kolejki magazynu dla nowego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="67b0f-199">This function processes name and address information dropped into Queue storage for a new user.</span></span>

> [!NOTE]
> <span data-ttu-id="67b0f-200">Jeśli używasz innej kolejki upewnij się, należy użyć nazwy hello zgodne toohello [nazewnictwo kolejek i metadanych](https://msdn.microsoft.com/library/dd179349.aspx) reguły.</span><span class="sxs-lookup"><span data-stu-id="67b0f-200">If you use a different queue name, make sure hello name you use conforms toohello [Naming Queues and MetaData](https://msdn.microsoft.com/library/dd179349.aspx) rules.</span></span> <span data-ttu-id="67b0f-201">W przeciwnym razie wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="67b0f-201">Otherwise, you get an error.</span></span>
>
>

1. <span data-ttu-id="67b0f-202">W hello [portalu Azure] dla funkcji aplikacji, kliknij przycisk **nową funkcję** > **QueueTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="67b0f-202">In hello [Azure portal] for your function app, click **New Function** > **QueueTrigger - C#**.</span></span>
2. <span data-ttu-id="67b0f-203">Wprowadź toobe nazwę kolejki hello monitorowane przez funkcję kolejki hello:</span><span class="sxs-lookup"><span data-stu-id="67b0f-203">Enter hello queue name toobe monitored by hello queue function:</span></span>

        queue-newusers
3. <span data-ttu-id="67b0f-204">Kliknij przycisk hello  **+**  przycisk tooselect lub utworzyć konto magazynu hello ma toouse.</span><span class="sxs-lookup"><span data-stu-id="67b0f-204">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="67b0f-205">Następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="67b0f-205">Then click **Create**.</span></span>
4. <span data-ttu-id="67b0f-206">Pozostaw to okno przeglądarki w portalu otwarty, więc można monitorować hello wpisy dziennika dla kodu szablonu funkcji hello domyślne kolejki.</span><span class="sxs-lookup"><span data-stu-id="67b0f-206">Leave this portal browser window open, so you can monitor hello log entries for hello default queue function template code.</span></span>

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a><span data-ttu-id="67b0f-207">Utwórz wiadomość w kolejce hello toodrop wyzwalacza czasomierza</span><span class="sxs-lookup"><span data-stu-id="67b0f-207">Create a timer trigger toodrop a message in hello queue</span></span>
1. <span data-ttu-id="67b0f-208">Otwórz hello [portalu Azure] w nowym oknie przeglądarki i przejdź tooyour funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67b0f-208">Open hello [Azure portal] in a new browser window, and navigate tooyour function app.</span></span>
2. <span data-ttu-id="67b0f-209">Kliknij przycisk **nową funkcję** > **TimerTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="67b0f-209">Click **New Function** > **TimerTrigger - C#**.</span></span> <span data-ttu-id="67b0f-210">Wprowadź tooset wyrażenie cron częstotliwość hello kodu czasomierza testów funkcji kolejki.</span><span class="sxs-lookup"><span data-stu-id="67b0f-210">Enter a cron expression tooset how often hello timer code tests your queue function.</span></span> <span data-ttu-id="67b0f-211">Następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="67b0f-211">Then click **Create**.</span></span> <span data-ttu-id="67b0f-212">Jeśli chcesz toorun testu hello co 30 sekund, można użyć następujących hello [wyrażenie CRON](https://wikipedia.org/wiki/Cron#CRON_expression):</span><span class="sxs-lookup"><span data-stu-id="67b0f-212">If you want hello test toorun every 30 seconds, you can use hello following [CRON expression](https://wikipedia.org/wiki/Cron#CRON_expression):</span></span>

        */30 * * * * *
3. <span data-ttu-id="67b0f-213">Kliknij przycisk hello **integracji** kartę nowego wyzwalacza czasomierza.</span><span class="sxs-lookup"><span data-stu-id="67b0f-213">Click hello **Integrate** tab for your new timer trigger.</span></span>
4. <span data-ttu-id="67b0f-214">W obszarze **dane wyjściowe**, kliknij przycisk **+ nowe dane wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="67b0f-214">Under **Output**, click **+ New Output**.</span></span> <span data-ttu-id="67b0f-215">Następnie kliknij przycisk **kolejki** i **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="67b0f-215">Then click **queue** and **Select**.</span></span>
5. <span data-ttu-id="67b0f-216">Uwaga hello nazwa używana dla hello **obiekt kolejki wiadomości**.</span><span class="sxs-lookup"><span data-stu-id="67b0f-216">Note hello name you use for hello **queue message object**.</span></span> <span data-ttu-id="67b0f-217">Możesz użyć tego hello czasomierza funkcja kodu.</span><span class="sxs-lookup"><span data-stu-id="67b0f-217">You use this in hello timer function code.</span></span>

        myQueue
6. <span data-ttu-id="67b0f-218">Wprowadź nazwę kolejki hello, w którym zostanie wysłana wiadomość hello:</span><span class="sxs-lookup"><span data-stu-id="67b0f-218">Enter hello queue name where hello message is sent:</span></span>

        queue-newusers
7. <span data-ttu-id="67b0f-219">Kliknij przycisk hello  **+**  przycisk konta magazynu hello tooselect wcześniej używany z wyzwalaczem kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="67b0f-219">Click hello **+** button tooselect hello storage account you used previously with hello queue trigger.</span></span> <span data-ttu-id="67b0f-220">Następnie kliknij przycisk **Save** (Zapisz).</span><span class="sxs-lookup"><span data-stu-id="67b0f-220">Then click **Save**.</span></span>
8. <span data-ttu-id="67b0f-221">Kliknij przycisk hello **opracowanie** kartę wyzwalacza czasomierza.</span><span class="sxs-lookup"><span data-stu-id="67b0f-221">Click hello **Develop** tab for your timer trigger.</span></span>
9. <span data-ttu-id="67b0f-222">Witaj następującego kodu dla funkcji czasomierza hello C#, można użyć tak długo, jak używane hello kolejka sama nazwa obiektu komunikatu przedstawiona wcześniej.</span><span class="sxs-lookup"><span data-stu-id="67b0f-222">You can use hello following code for hello C# timer function, as long as you used hello same queue message object name shown earlier.</span></span> <span data-ttu-id="67b0f-223">Następnie kliknij przycisk **Save** (Zapisz).</span><span class="sxs-lookup"><span data-stu-id="67b0f-223">Then click **Save**.</span></span>

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

<span data-ttu-id="67b0f-224">W tym momencie hello funkcja czasomierza C# wykonuje co 30 sekund, jeśli użyto wyrażenia cron przykład hello.</span><span class="sxs-lookup"><span data-stu-id="67b0f-224">At this point, hello C# timer function executes every 30 seconds if you used hello example cron expression.</span></span> <span data-ttu-id="67b0f-225">Dzienniki Hello funkcji czasomierza hello raport Każde wykonanie:</span><span class="sxs-lookup"><span data-stu-id="67b0f-225">hello logs for hello timer function report each execution:</span></span>

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

<span data-ttu-id="67b0f-226">W oknie przeglądarki hello hello kolejki funkcji można wyświetlić każdego przetwarzanego komunikatu:</span><span class="sxs-lookup"><span data-stu-id="67b0f-226">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a><span data-ttu-id="67b0f-227">Testowanie funkcji z kodu</span><span class="sxs-lookup"><span data-stu-id="67b0f-227">Test a function with code</span></span>
<span data-ttu-id="67b0f-228">Toocreate zewnętrznych aplikacji lub framework tootest może być konieczne funkcji.</span><span class="sxs-lookup"><span data-stu-id="67b0f-228">You may need toocreate an external application or framework tootest your functions.</span></span>

### <a name="test-an-http-trigger-function-with-code-nodejs"></a><span data-ttu-id="67b0f-229">Testowanie funkcji wyzwalacza HTTP o kodzie: Node.js</span><span class="sxs-lookup"><span data-stu-id="67b0f-229">Test an HTTP trigger function with code: Node.js</span></span>
<span data-ttu-id="67b0f-230">Tooexecute aplikacji Node.js tootest żądania HTTP można użyć funkcji.</span><span class="sxs-lookup"><span data-stu-id="67b0f-230">You can use a Node.js app tooexecute an HTTP request tootest your function.</span></span>
<span data-ttu-id="67b0f-231">Upewnij się, że tooset:</span><span class="sxs-lookup"><span data-stu-id="67b0f-231">Make sure tooset:</span></span>

* <span data-ttu-id="67b0f-232">Witaj `host` hello żądania opcje tooyour funkcji aplikacji hosta.</span><span class="sxs-lookup"><span data-stu-id="67b0f-232">hello `host` in hello request options tooyour function app host.</span></span>
* <span data-ttu-id="67b0f-233">Nazwa funkcji programu hello `path`.</span><span class="sxs-lookup"><span data-stu-id="67b0f-233">Your function name in hello `path`.</span></span>
* <span data-ttu-id="67b0f-234">Kod dostępu (`<your code>`) w hello `path`.</span><span class="sxs-lookup"><span data-stu-id="67b0f-234">Your access code (`<your code>`) in hello `path`.</span></span>

<span data-ttu-id="67b0f-235">Przykład kodu:</span><span class="sxs-lookup"><span data-stu-id="67b0f-235">Code example:</span></span>

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


<span data-ttu-id="67b0f-236">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="67b0f-236">Output:</span></span>

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

<span data-ttu-id="67b0f-237">W portalu hello **dzienniki** okno dane wyjściowe podobne następujące toohello jest rejestrowane podczas wykonywania funkcji hello:</span><span class="sxs-lookup"><span data-stu-id="67b0f-237">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a><span data-ttu-id="67b0f-238">Testowanie funkcji wyzwalacza kolejki z kodem: C#</span><span class="sxs-lookup"><span data-stu-id="67b0f-238">Test a queue trigger function with code: C#</span></span> #
<span data-ttu-id="67b0f-239">Wspomniano wcześniej przetestowanie wyzwalacz kolejki przy użyciu kodu toodrop wiadomości w swojej kolejki.</span><span class="sxs-lookup"><span data-stu-id="67b0f-239">We mentioned earlier that you can test a queue trigger by using code toodrop a message in your queue.</span></span> <span data-ttu-id="67b0f-240">Witaj następującego przykładowego kodu jest oparta na powitania C# kod przedstawiony w hello [Rozpoczynanie pracy z magazynem kolejek Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="67b0f-240">hello following example code is based on hello C# code presented in hello [Getting started with Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span></span> <span data-ttu-id="67b0f-241">Kod dla innych języków jest również dostępna z tego łącza.</span><span class="sxs-lookup"><span data-stu-id="67b0f-241">Code for other languages is also available from that link.</span></span>

<span data-ttu-id="67b0f-242">tootest tego kodu w aplikacji konsoli, musi:</span><span class="sxs-lookup"><span data-stu-id="67b0f-242">tootest this code in a console app, you must:</span></span>

* <span data-ttu-id="67b0f-243">[Konfigurowanie parametrów połączenia magazynu w pliku app.config hello](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="67b0f-243">[Configure your storage connection string in hello app.config file](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>
* <span data-ttu-id="67b0f-244">Przekaż `name` i `address` jako parametry toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67b0f-244">Pass a `name` and `address` as parameters toohello app.</span></span> <span data-ttu-id="67b0f-245">Na przykład `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span><span class="sxs-lookup"><span data-stu-id="67b0f-245">For example, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span></span> <span data-ttu-id="67b0f-246">(Ten kod akceptuje hello nazwę i adres dla nowego użytkownika jako argumenty wiersza polecenia w czasie wykonywania.)</span><span class="sxs-lookup"><span data-stu-id="67b0f-246">(This code accepts hello name and address for a new user as command-line arguments during runtime.)</span></span>

<span data-ttu-id="67b0f-247">Przykład C# kodu:</span><span class="sxs-lookup"><span data-stu-id="67b0f-247">Example C# code:</span></span>

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

<span data-ttu-id="67b0f-248">W oknie przeglądarki hello hello kolejki funkcji można wyświetlić każdego przetwarzanego komunikatu:</span><span class="sxs-lookup"><span data-stu-id="67b0f-248">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[portalu Azure]: https://portal.azure.com
