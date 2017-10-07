---
title: definicje aaaCustomize generowanych przez pakiet Swashbuckle interfejsu API
description: "Dowiedz się, jak toocustomize definicji interfejsu API programu Swagger, które są generowane przez pakiet Swashbuckle dla aplikacji interfejsu API w usłudze Azure App Service."
services: app-service\api
documentationcenter: .net
author: bradygaster
manager: erikre
editor: jimbe
ms.assetid: 6b8cbc38-d282-4a0f-b0c5-762631bae6f3
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: e31c665f8993533c5ec9a935e42cce34f86a5ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-swashbuckle-generated-api-definitions"></a><span data-ttu-id="d828a-103">Dostosowywanie definicji wygenerowanych przez pakiet Swashbuckle interfejsu API</span><span class="sxs-lookup"><span data-stu-id="d828a-103">Customize Swashbuckle-generated API definitions</span></span>
## <a name="overview"></a><span data-ttu-id="d828a-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="d828a-104">Overview</span></span>
<span data-ttu-id="d828a-105">W tym artykule opisano sposób toocustomize Swashbuckle toohandle typowych scenariuszy może miejscu tooalter hello domyślne zachowanie:</span><span class="sxs-lookup"><span data-stu-id="d828a-105">This article explains how toocustomize Swashbuckle toohandle common scenarios where you may want tooalter hello default behavior:</span></span>

* <span data-ttu-id="d828a-106">Pakiet Swashbuckle generuje operacji zduplikowane identyfikatory przeciążenia metody kontrolera</span><span class="sxs-lookup"><span data-stu-id="d828a-106">Swashbuckle generates duplicate operation identifiers for overloads of controller methods</span></span>
* <span data-ttu-id="d828a-107">Pakiet Swashbuckle zakłada tego hello tylko prawidłowej odpowiedzi z metody jest 200 protokołu HTTP (OK)</span><span class="sxs-lookup"><span data-stu-id="d828a-107">Swashbuckle assumes that hello only valid response from a method is HTTP 200 (OK)</span></span> 

## <a name="customize-operation-identifier-generation"></a><span data-ttu-id="d828a-108">Dostosowywanie generowania identyfikatora operacji</span><span class="sxs-lookup"><span data-stu-id="d828a-108">Customize operation identifier generation</span></span>
<span data-ttu-id="d828a-109">Swashbuckle generuje identyfikatory operacji programu Swagger, łącząc nazwy kontrolera i nazwy metody.</span><span class="sxs-lookup"><span data-stu-id="d828a-109">Swashbuckle generates Swagger operation identifiers by concatenating controller name and method name.</span></span> <span data-ttu-id="d828a-110">Ten wzorzec tworzy problem, jeśli masz wiele przeciążenia metody: Swashbuckle generuje operacji zduplikowane identyfikatory, która jest nieprawidłowa JSON programu Swagger.</span><span class="sxs-lookup"><span data-stu-id="d828a-110">This pattern creates a problem when you have multiple overloads of a method: Swashbuckle generates duplicate operation ids, which is invalid Swagger JSON.</span></span>

<span data-ttu-id="d828a-111">Na przykład hello następującego kodu kontrolera powoduje Swashbuckle toogenerate trzy Contact_Get identyfikatory operacji.</span><span class="sxs-lookup"><span data-stu-id="d828a-111">For example, hello following controller code causes Swashbuckle toogenerate three Contact_Get operation ids.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

<span data-ttu-id="d828a-112">Witaj problem można rozwiązać ręcznie, zapewniając metody hello unikatowe nazwy, takie jak następujące hello w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="d828a-112">You can solve hello problem manually by giving hello methods unique names, such as hello following for this example:</span></span>

* <span data-ttu-id="d828a-113">Get</span><span class="sxs-lookup"><span data-stu-id="d828a-113">Get</span></span>
* <span data-ttu-id="d828a-114">GetById</span><span class="sxs-lookup"><span data-stu-id="d828a-114">GetById</span></span>
* <span data-ttu-id="d828a-115">GetPage</span><span class="sxs-lookup"><span data-stu-id="d828a-115">GetPage</span></span>

<span data-ttu-id="d828a-116">Alternatywą Hello jest toomake Swashbuckle tooextend automatycznego generowania operacji unikatowych identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="d828a-116">hello alternative is tooextend Swashbuckle toomake it automatically generate unique operation ids.</span></span>

<span data-ttu-id="d828a-117">Witaj poniższej procedurze pokazano, jak hello toocustomize Swashbuckle za pomocą *SwaggerConfig.cs* pliku, który znajduje się w projekcie hello przez szablon projektu Visual Studio interfejsu API Apps Preview hello.</span><span class="sxs-lookup"><span data-stu-id="d828a-117">hello following steps show how toocustomize Swashbuckle by using hello *SwaggerConfig.cs* file that is included in hello project by hello Visual Studio API Apps Preview project template.</span></span>  <span data-ttu-id="d828a-118">Można również dostosować Swashbuckle w projekcie interfejsu API sieci Web skonfigurowana dla wdrażania aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d828a-118">You can also customize Swashbuckle in a Web API project that you configure for deployment as an API app.</span></span>

1. <span data-ttu-id="d828a-119">Utworzenie niestandardowego `IOperationFilter` implementacji</span><span class="sxs-lookup"><span data-stu-id="d828a-119">Create a custom `IOperationFilter` implementation</span></span> 
   
    <span data-ttu-id="d828a-120">Witaj `IOperationFilter` interfejsu udostępnia punkt rozszerzalności dla Swashbuckle użytkowników, którzy chcą toocustomize różnych aspektów procesu metadanych struktury Swagger hello.</span><span class="sxs-lookup"><span data-stu-id="d828a-120">hello `IOperationFilter` interface provides an extensibility point for Swashbuckle users who want toocustomize various aspects of hello Swagger metadata process.</span></span> <span data-ttu-id="d828a-121">Witaj poniższy kod przedstawia jedną z metod zmiany zachowania operacji identyfikator generacji hello.</span><span class="sxs-lookup"><span data-stu-id="d828a-121">hello following code demonstrates one method of changing hello operation-id-generation behavior.</span></span> <span data-ttu-id="d828a-122">Kod Hello dołącza nazwy identyfikatora operacji toohello nazwy parametru.</span><span class="sxs-lookup"><span data-stu-id="d828a-122">hello code appends parameter names toohello operation id name.</span></span>  
   
        using Swashbuckle.Swagger;
        using System.Web.Http.Description;
   
        namespace ContactsList
        {
            public class MultipleOperationsWithSameVerbFilter : IOperationFilter
            {
                public void Apply(
                    Operation operation,
                    SchemaRegistry schemaRegistry,
                    ApiDescription apiDescription)
                {
                    if (operation.parameters != null)
                    {
                        operation.operationId += "By";
                        foreach (var parm in operation.parameters)
                        {
                            operation.operationId += string.Format("{0}",parm.name);
                        }
                    }
                }
            }
        }
2. <span data-ttu-id="d828a-123">W *App_Start\SwaggerConfig.cs* plik, hello wywołania `OperationFilter` metody toocause Swashbuckle toouse hello nowe `IOperationFilter` implementacji.</span><span class="sxs-lookup"><span data-stu-id="d828a-123">In *App_Start\SwaggerConfig.cs* file, call hello `OperationFilter` method toocause Swashbuckle toouse hello new `IOperationFilter` implementation.</span></span>
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    <span data-ttu-id="d828a-124">Witaj *SwaggerConfig.cs* plików, które są przenoszone przez hello pakietu Swashbuckle NuGet zawiera wiele przykładów poza komentarzem punkty rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="d828a-124">hello *SwaggerConfig.cs* file that is dropped in by hello Swashbuckle NuGet package contains many commented-out examples of extensibility points.</span></span> <span data-ttu-id="d828a-125">dodatkowe uwagi Hello nie są wyświetlane tutaj.</span><span class="sxs-lookup"><span data-stu-id="d828a-125">hello additional comments are not shown here.</span></span> 
   
    <span data-ttu-id="d828a-126">Po wprowadzeniu tej zmiany z `IOperationFilter` implementacji jest używana i powoduje, że operacja unikatowe identyfikatory toobe generowane.</span><span class="sxs-lookup"><span data-stu-id="d828a-126">After you make this change, your `IOperationFilter` implementation is used and causes unique operation ids toobe generated.</span></span>
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a><span data-ttu-id="d828a-127">Zezwalaj na kody odpowiedzi innych niż 200</span><span class="sxs-lookup"><span data-stu-id="d828a-127">Allow response codes other than 200</span></span>
<span data-ttu-id="d828a-128">Domyślnie pakiet Swashbuckle zakłada, że odpowiedź 200 protokołu HTTP (OK) hello *tylko* prawnie odpowiedzi z metody interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d828a-128">By default, Swashbuckle assumes that an HTTP 200 (OK) response is hello *only* legitimate response from a Web API method.</span></span> <span data-ttu-id="d828a-129">W niektórych przypadkach może być tooreturn innych kodów odpowiedzi bez powodowania powitania klienta tooraise Wystąpił wyjątek.</span><span class="sxs-lookup"><span data-stu-id="d828a-129">In some cases, you may want tooreturn other response codes without causing hello client tooraise an exception.</span></span>  <span data-ttu-id="d828a-130">Na przykład hello następującego kodu interfejsu API sieci Web przedstawiono scenariusz, w którym można powitania klienta tooaccept 200 lub 404 jako prawidłowy odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d828a-130">For example, hello following Web API code demonstrates a scenario in which you would want hello client tooaccept either a 200 or a 404 as valid responses.</span></span>

    [ResponseType(typeof(Contact))]
    public HttpResponseMessage Get(int id)
    {
        var contacts = GetContacts();

        var requestedContact = contacts.FirstOrDefault(x => x.Id == id);

        if (requestedContact == null)
        {
            return Request.CreateResponse(HttpStatusCode.NotFound);
        }
        else
        {
            return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
        }
    }

<span data-ttu-id="d828a-131">W tym scenariuszu hello programu Swagger, który Swashbuckle generuje domyślnie określa tylko jeden uzasadnionych kod stanu HTTP, 200 protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="d828a-131">In this scenario, hello Swagger that Swashbuckle generates by default specifies only one legitimate HTTP status code, HTTP 200.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

<span data-ttu-id="d828a-132">Ponieważ program Visual Studio korzysta hello kodu toogenerate definicji interfejsu API programu Swagger dla powitania klienta, tworzy kod klienta, który zgłasza wyjątek dla odpowiedzi innych niż 200 protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="d828a-132">Since Visual Studio uses hello Swagger API definition toogenerate code for hello client, it creates client code that raises an exception for any response other than an HTTP 200.</span></span> <span data-ttu-id="d828a-133">Poniższy kod Hello jest w kliencie C# wygenerowany dla tej próbki metody interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d828a-133">hello code below is from a C# client generated for this sample Web API method.</span></span>

    if (statusCode != HttpStatusCode.OK)
    {
        HttpOperationException<object> ex = new HttpOperationException<object>();
        ex.Request = httpRequest;
        ex.Response = httpResponse;
        ex.Body = null;
        if (shouldTrace)
        {
            ServiceClientTracing.Error(invocationId, ex);
        }
        throw ex;
    } 

<span data-ttu-id="d828a-134">Pakiet Swashbuckle udostępnia dwa sposoby dostosowywania hello Lista oczekiwanych kody odpowiedzi HTTP, które generuje przy użyciu komentarze XML lub hello `SwaggerResponse` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="d828a-134">Swashbuckle provides two ways of customizing hello list of expected HTTP response codes that it generates, using XML comments or hello `SwaggerResponse` attribute.</span></span> <span data-ttu-id="d828a-135">Atrybut Hello jest łatwiejsze, ale tylko jest dostępna w Swashbuckle 5.1.5 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d828a-135">hello attribute is easier, but it is only available in Swashbuckle 5.1.5 or later.</span></span> <span data-ttu-id="d828a-136">Hello aplikacje interfejsu API Podgląd nowego projektu szablon programu Visual Studio 2013 zawiera Swashbuckle wersji 5.0.0, jeśli więc użyć szablonu hello i nie mają tooupdate Swashbuckle, jedyną opcją toouse komentarze XML.</span><span class="sxs-lookup"><span data-stu-id="d828a-136">hello API Apps preview new-project template in Visual Studio 2013 includes Swashbuckle version 5.0.0, so if you used hello template and don't want tooupdate Swashbuckle, your only option is toouse XML comments.</span></span> 

### <a name="customize-expected-response-codes-using-xml-comments"></a><span data-ttu-id="d828a-137">Dostosowywanie kodów odpowiedzi oczekiwanego przy użyciu komentarze XML</span><span class="sxs-lookup"><span data-stu-id="d828a-137">Customize expected response codes using XML comments</span></span>
<span data-ttu-id="d828a-138">Kody odpowiedzi toospecify tej metody należy używać, jeśli pakiet Swashbuckle wersja jest wcześniejsza niż 5.1.5.</span><span class="sxs-lookup"><span data-stu-id="d828a-138">Use this method toospecify response codes if your Swashbuckle version is earlier than 5.1.5.</span></span>

1. <span data-ttu-id="d828a-139">Najpierw dodaj komentarze dokumentacji XML zamiast metod hello, które mają toospecify kodów odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="d828a-139">First, add XML documentation comments over hello methods you wish toospecify HTTP response codes for.</span></span> <span data-ttu-id="d828a-140">Biorąc hello przykładowy interfejs API sieci Web działania, które spowoduje tooit dokumentacji XML hello przedstawionych powyżej i mające zastosowanie w kodzie, takich jak hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="d828a-140">Taking hello sample Web API action shown above and applying hello XML documentation tooit would result in code like hello following example.</span></span> 
   
        /// <summary>
        /// Returns hello specified contact.
        /// </summary>
        /// <param name="id">hello ID of hello contact.</param>
        /// <returns>A contact record with an HTTP 200, or null with an HTTP 404.</returns>
        /// <response code="200">OK</response>
        /// <response code="404">Not Found</response>
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
   
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
2. <span data-ttu-id="d828a-141">Dodaj instrukcje w hello *SwaggerConfig.cs* toodirect Swashbuckle toomake użycie pliku dokumentacji XML hello pliku.</span><span class="sxs-lookup"><span data-stu-id="d828a-141">Add instructions in hello *SwaggerConfig.cs* file toodirect Swashbuckle toomake use of hello XML documentation file.</span></span>
   
   * <span data-ttu-id="d828a-142">Otwórz *SwaggerConfig.cs* i utworzyć metodę na powitania *SwaggerConfig* hello toospecify klasy ścieżka pliku XML dokumentacji toohello.</span><span class="sxs-lookup"><span data-stu-id="d828a-142">Open *SwaggerConfig.cs* and create a method on hello *SwaggerConfig* class toospecify hello path toohello documentation XML file.</span></span> 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * <span data-ttu-id="d828a-143">Przewiń w dół w hello *SwaggerConfig.cs* pliku, aż zostanie wyświetlony wiersz poza komentarzem hello kodu przypominającą ekranie powitania zrzut poniżej.</span><span class="sxs-lookup"><span data-stu-id="d828a-143">Scroll down in hello *SwaggerConfig.cs* file until you see hello commented-out line of code resembling hello screen shot below.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * <span data-ttu-id="d828a-144">Usuń znaczniki komentarza hello wiersz tooenable hello XML komentarze przetwarzania podczas generowania struktury Swagger.</span><span class="sxs-lookup"><span data-stu-id="d828a-144">Uncomment hello line tooenable hello XML comments processing during Swagger generation.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. <span data-ttu-id="d828a-145">W kolejności toogenerate hello pliku XML dokumentacji przejdź do właściwości projektu hello i Włącz hello pliku dokumentacji XML jak pokazano na poniższym zrzucie ekranu hello.</span><span class="sxs-lookup"><span data-stu-id="d828a-145">In order toogenerate hello XML documentation file, go into hello project's properties and enable hello XML documentation file as shown in hello screenshot below.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

<span data-ttu-id="d828a-146">Po wykonaniu tych kroków hello JSON programu Swagger generowane przez pakiet Swashbuckle, zostaną one zastosowane hello kody odpowiedzi HTTP, określonych w komentarzach XML hello.</span><span class="sxs-lookup"><span data-stu-id="d828a-146">Once you perform these steps, hello Swagger JSON generated by Swashbuckle will reflect hello HTTP response codes that you specified in hello XML comments.</span></span> <span data-ttu-id="d828a-147">Poniższy zrzut ekranu Hello przedstawiono ten nowy ładunek JSON.</span><span class="sxs-lookup"><span data-stu-id="d828a-147">hello screenshot below demonstrates this new JSON payload.</span></span> 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

<span data-ttu-id="d828a-148">Korzystając z programu Visual Studio tooregenerate powitania klienta kodu do interfejsu API REST, hello kod w języku C# akceptuje zarówno hello HTTP OK i nie można odnaleźć stanu kody bez podnoszenia wyjątek, umożliwiając odbierającą decyzji dotyczących toomake kodu, w sposób toohandle hello zwracają wartość null Skontaktuj się z rekordu.</span><span class="sxs-lookup"><span data-stu-id="d828a-148">When you use Visual Studio tooregenerate hello client code for your REST API, hello C# code accepts both hello HTTP OK and Not Found status codes without raising an exception, allowing your consuming code toomake decisions on how toohandle hello return of a null Contact record.</span></span> 

        if (statusCode != HttpStatusCode.OK && statusCode != HttpStatusCode.NotFound)
        {
            HttpOperationException<object> ex = new HttpOperationException<object>();
            ex.Request = httpRequest;
            ex.Response = httpResponse;
            ex.Body = null;
            if (shouldTrace)
            {
                ServiceClientTracing.Error(invocationId, ex);
            }
                throw ex;
        }

<span data-ttu-id="d828a-149">Kod Hello tej prezentacji można znaleźć w [to repozytorium GitHub](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse).</span><span class="sxs-lookup"><span data-stu-id="d828a-149">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse).</span></span> <span data-ttu-id="d828a-150">Wraz z hello interfejsu API sieci Web projektu oznaczonych komentarze dokumentacji XML jest projekt aplikacji konsoli, który zawiera wygenerowanego klienta dla tego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d828a-150">Along with hello Web API project marked up with XML documentation comments is a Console Application project that contains a generated client for this API.</span></span> 

### <a name="customize-expected-response-codes-using-hello-swaggerresponse-attribute"></a><span data-ttu-id="d828a-151">Dostosowywanie kodów odpowiedzi oczekiwanego przy użyciu atrybutu SwaggerResponse hello</span><span class="sxs-lookup"><span data-stu-id="d828a-151">Customize expected response codes using hello SwaggerResponse attribute</span></span>
<span data-ttu-id="d828a-152">Witaj [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) atrybutu jest dostępna w Swashbuckle 5.1.5 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d828a-152">hello [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) attribute is available in Swashbuckle 5.1.5 and later.</span></span> <span data-ttu-id="d828a-153">W przypadku, gdy w projekcie jest zainstalowana starsza wersja tej sekcji rozpoczyna się od wyjaśniający, jak hello tooupdate Swashbuckle NuGet pakietu, dzięki czemu można użyć tego atrybutu.</span><span class="sxs-lookup"><span data-stu-id="d828a-153">In case you have an earlier version in your project, this section starts by explaining how tooupdate hello Swashbuckle NuGet package so that you can use this attribute.</span></span>

1. <span data-ttu-id="d828a-154">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt interfejsu API sieci Web i kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d828a-154">In **Solution Explorer**, right-click your Web API project and click **Manage NuGet Packages**.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. <span data-ttu-id="d828a-155">Kliknij przycisk hello *aktualizacji* przycisku Dalej toohello *Swashbuckle* pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="d828a-155">Click hello *Update* button next toohello *Swashbuckle* NuGet package.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. <span data-ttu-id="d828a-156">Dodaj hello *SwaggerResponse* atrybuty akcji metody interfejsu API sieci Web toohello, dla których chcesz toospecify prawidłowe kody odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="d828a-156">Add hello *SwaggerResponse* attributes toohello Web API action methods for which you want toospecify valid HTTP response codes.</span></span> 
   
        [SwaggerResponse(HttpStatusCode.OK)]
        [SwaggerResponse(HttpStatusCode.NotFound)]
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
4. <span data-ttu-id="d828a-157">Dodaj `using` instrukcji hello atrybutu przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="d828a-157">Add a `using` statement for hello attribute's namespace:</span></span>
   
        using Swashbuckle.Swagger.Annotations;
5. <span data-ttu-id="d828a-158">Przeglądaj toohello */swagger/docs/v1* adres URL projektu i hello różnych kodów odpowiedzi HTTP będzie widoczny w hello JSON programu Swagger.</span><span class="sxs-lookup"><span data-stu-id="d828a-158">Browse toohello */swagger/docs/v1* URL of your project and hello various HTTP response codes will be visible in hello Swagger JSON.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

<span data-ttu-id="d828a-159">Kod Hello tej prezentacji można znaleźć w [to repozytorium GitHub](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes).</span><span class="sxs-lookup"><span data-stu-id="d828a-159">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes).</span></span> <span data-ttu-id="d828a-160">Wraz z hello projekt interfejsu API sieci Web ozdobione hello *SwaggerResponse* atrybut jest projekt aplikacji konsoli, który zawiera wygenerowanego klienta dla tego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d828a-160">Along with hello Web API project decorated with hello *SwaggerResponse* attribute is a Console Application project that contains a generated client for this API.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d828a-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d828a-161">Next steps</span></span>
<span data-ttu-id="d828a-162">W tym artykule pokazuje, jak sposób hello toocustomize Swashbuckle generuje identyfikatorów operacji i kody prawidłowej odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d828a-162">This article has shown how toocustomize hello way Swashbuckle generates operation ids and valid response codes.</span></span> <span data-ttu-id="d828a-163">Aby uzyskać więcej informacji, zobacz [Swashbuckle w serwisie GitHub](https://github.com/domaindrivendev/Swashbuckle).</span><span class="sxs-lookup"><span data-stu-id="d828a-163">For more information, see [Swashbuckle on GitHub](https://github.com/domaindrivendev/Swashbuckle).</span></span>

