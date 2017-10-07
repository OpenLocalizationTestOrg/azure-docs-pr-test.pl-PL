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
# <a name="customize-swashbuckle-generated-api-definitions"></a>Dostosowywanie definicji wygenerowanych przez pakiet Swashbuckle interfejsu API
## <a name="overview"></a>Omówienie
W tym artykule opisano sposób toocustomize Swashbuckle toohandle typowych scenariuszy może miejscu tooalter hello domyślne zachowanie:

* Pakiet Swashbuckle generuje operacji zduplikowane identyfikatory przeciążenia metody kontrolera
* Pakiet Swashbuckle zakłada tego hello tylko prawidłowej odpowiedzi z metody jest 200 protokołu HTTP (OK) 

## <a name="customize-operation-identifier-generation"></a>Dostosowywanie generowania identyfikatora operacji
Swashbuckle generuje identyfikatory operacji programu Swagger, łącząc nazwy kontrolera i nazwy metody. Ten wzorzec tworzy problem, jeśli masz wiele przeciążenia metody: Swashbuckle generuje operacji zduplikowane identyfikatory, która jest nieprawidłowa JSON programu Swagger.

Na przykład hello następującego kodu kontrolera powoduje Swashbuckle toogenerate trzy Contact_Get identyfikatory operacji.

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

Witaj problem można rozwiązać ręcznie, zapewniając metody hello unikatowe nazwy, takie jak następujące hello w tym przykładzie:

* Get
* GetById
* GetPage

Alternatywą Hello jest toomake Swashbuckle tooextend automatycznego generowania operacji unikatowych identyfikatorów.

Witaj poniższej procedurze pokazano, jak hello toocustomize Swashbuckle za pomocą *SwaggerConfig.cs* pliku, który znajduje się w projekcie hello przez szablon projektu Visual Studio interfejsu API Apps Preview hello.  Można również dostosować Swashbuckle w projekcie interfejsu API sieci Web skonfigurowana dla wdrażania aplikacji interfejsu API.

1. Utworzenie niestandardowego `IOperationFilter` implementacji 
   
    Witaj `IOperationFilter` interfejsu udostępnia punkt rozszerzalności dla Swashbuckle użytkowników, którzy chcą toocustomize różnych aspektów procesu metadanych struktury Swagger hello. Witaj poniższy kod przedstawia jedną z metod zmiany zachowania operacji identyfikator generacji hello. Kod Hello dołącza nazwy identyfikatora operacji toohello nazwy parametru.  
   
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
2. W *App_Start\SwaggerConfig.cs* plik, hello wywołania `OperationFilter` metody toocause Swashbuckle toouse hello nowe `IOperationFilter` implementacji.
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    Witaj *SwaggerConfig.cs* plików, które są przenoszone przez hello pakietu Swashbuckle NuGet zawiera wiele przykładów poza komentarzem punkty rozszerzeń. dodatkowe uwagi Hello nie są wyświetlane tutaj. 
   
    Po wprowadzeniu tej zmiany z `IOperationFilter` implementacji jest używana i powoduje, że operacja unikatowe identyfikatory toobe generowane.
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a>Zezwalaj na kody odpowiedzi innych niż 200
Domyślnie pakiet Swashbuckle zakłada, że odpowiedź 200 protokołu HTTP (OK) hello *tylko* prawnie odpowiedzi z metody interfejsu API sieci Web. W niektórych przypadkach może być tooreturn innych kodów odpowiedzi bez powodowania powitania klienta tooraise Wystąpił wyjątek.  Na przykład hello następującego kodu interfejsu API sieci Web przedstawiono scenariusz, w którym można powitania klienta tooaccept 200 lub 404 jako prawidłowy odpowiedzi.

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

W tym scenariuszu hello programu Swagger, który Swashbuckle generuje domyślnie określa tylko jeden uzasadnionych kod stanu HTTP, 200 protokołu HTTP.

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

Ponieważ program Visual Studio korzysta hello kodu toogenerate definicji interfejsu API programu Swagger dla powitania klienta, tworzy kod klienta, który zgłasza wyjątek dla odpowiedzi innych niż 200 protokołu HTTP. Poniższy kod Hello jest w kliencie C# wygenerowany dla tej próbki metody interfejsu API sieci Web.

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

Pakiet Swashbuckle udostępnia dwa sposoby dostosowywania hello Lista oczekiwanych kody odpowiedzi HTTP, które generuje przy użyciu komentarze XML lub hello `SwaggerResponse` atrybutu. Atrybut Hello jest łatwiejsze, ale tylko jest dostępna w Swashbuckle 5.1.5 lub nowszej. Hello aplikacje interfejsu API Podgląd nowego projektu szablon programu Visual Studio 2013 zawiera Swashbuckle wersji 5.0.0, jeśli więc użyć szablonu hello i nie mają tooupdate Swashbuckle, jedyną opcją toouse komentarze XML. 

### <a name="customize-expected-response-codes-using-xml-comments"></a>Dostosowywanie kodów odpowiedzi oczekiwanego przy użyciu komentarze XML
Kody odpowiedzi toospecify tej metody należy używać, jeśli pakiet Swashbuckle wersja jest wcześniejsza niż 5.1.5.

1. Najpierw dodaj komentarze dokumentacji XML zamiast metod hello, które mają toospecify kodów odpowiedzi HTTP. Biorąc hello przykładowy interfejs API sieci Web działania, które spowoduje tooit dokumentacji XML hello przedstawionych powyżej i mające zastosowanie w kodzie, takich jak hello poniższy przykład. 
   
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
2. Dodaj instrukcje w hello *SwaggerConfig.cs* toodirect Swashbuckle toomake użycie pliku dokumentacji XML hello pliku.
   
   * Otwórz *SwaggerConfig.cs* i utworzyć metodę na powitania *SwaggerConfig* hello toospecify klasy ścieżka pliku XML dokumentacji toohello. 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * Przewiń w dół w hello *SwaggerConfig.cs* pliku, aż zostanie wyświetlony wiersz poza komentarzem hello kodu przypominającą ekranie powitania zrzut poniżej. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * Usuń znaczniki komentarza hello wiersz tooenable hello XML komentarze przetwarzania podczas generowania struktury Swagger. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. W kolejności toogenerate hello pliku XML dokumentacji przejdź do właściwości projektu hello i Włącz hello pliku dokumentacji XML jak pokazano na poniższym zrzucie ekranu hello. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

Po wykonaniu tych kroków hello JSON programu Swagger generowane przez pakiet Swashbuckle, zostaną one zastosowane hello kody odpowiedzi HTTP, określonych w komentarzach XML hello. Poniższy zrzut ekranu Hello przedstawiono ten nowy ładunek JSON. 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

Korzystając z programu Visual Studio tooregenerate powitania klienta kodu do interfejsu API REST, hello kod w języku C# akceptuje zarówno hello HTTP OK i nie można odnaleźć stanu kody bez podnoszenia wyjątek, umożliwiając odbierającą decyzji dotyczących toomake kodu, w sposób toohandle hello zwracają wartość null Skontaktuj się z rekordu. 

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

Kod Hello tej prezentacji można znaleźć w [to repozytorium GitHub](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse). Wraz z hello interfejsu API sieci Web projektu oznaczonych komentarze dokumentacji XML jest projekt aplikacji konsoli, który zawiera wygenerowanego klienta dla tego interfejsu API. 

### <a name="customize-expected-response-codes-using-hello-swaggerresponse-attribute"></a>Dostosowywanie kodów odpowiedzi oczekiwanego przy użyciu atrybutu SwaggerResponse hello
Witaj [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) atrybutu jest dostępna w Swashbuckle 5.1.5 lub nowszej. W przypadku, gdy w projekcie jest zainstalowana starsza wersja tej sekcji rozpoczyna się od wyjaśniający, jak hello tooupdate Swashbuckle NuGet pakietu, dzięki czemu można użyć tego atrybutu.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt interfejsu API sieci Web i kliknij przycisk **Zarządzaj pakietami NuGet**. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. Kliknij przycisk hello *aktualizacji* przycisku Dalej toohello *Swashbuckle* pakietu NuGet. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. Dodaj hello *SwaggerResponse* atrybuty akcji metody interfejsu API sieci Web toohello, dla których chcesz toospecify prawidłowe kody odpowiedzi HTTP. 
   
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
4. Dodaj `using` instrukcji hello atrybutu przestrzeni nazw:
   
        using Swashbuckle.Swagger.Annotations;
5. Przeglądaj toohello */swagger/docs/v1* adres URL projektu i hello różnych kodów odpowiedzi HTTP będzie widoczny w hello JSON programu Swagger. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

Kod Hello tej prezentacji można znaleźć w [to repozytorium GitHub](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes). Wraz z hello projekt interfejsu API sieci Web ozdobione hello *SwaggerResponse* atrybut jest projekt aplikacji konsoli, który zawiera wygenerowanego klienta dla tego interfejsu API. 

## <a name="next-steps"></a>Następne kroki
W tym artykule pokazuje, jak sposób hello toocustomize Swashbuckle generuje identyfikatorów operacji i kody prawidłowej odpowiedzi. Aby uzyskać więcej informacji, zobacz [Swashbuckle w serwisie GitHub](https://github.com/domaindrivendev/Swashbuckle).

