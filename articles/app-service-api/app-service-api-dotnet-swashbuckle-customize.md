---
title: Dostosowywanie definicji wygenerowanych przez pakiet Swashbuckle interfejsu API
description: "Dowiedz się, jak dostosowywanie definicji interfejsu API programu Swagger, które są generowane przez pakiet Swashbuckle dla aplikacji interfejsu API w usłudze Azure App Service."
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
ms.openlocfilehash: c83905a97fb2ee988fe06fc1f9a7379c1741fd02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="customize-swashbuckle-generated-api-definitions"></a>Dostosowywanie definicji wygenerowanych przez pakiet Swashbuckle interfejsu API
## <a name="overview"></a>Omówienie
W tym artykule opisano sposób dostosowywania Swashbuckle do obsługi typowych scenariuszy, w którym może zajść potrzeba zmiany domyślnego zachowania:

* Pakiet Swashbuckle generuje operacji zduplikowane identyfikatory przeciążenia metody kontrolera
* Pakiet Swashbuckle zakłada, że tylko prawidłowej odpowiedzi z metody 200 protokołu HTTP (OK) 

## <a name="customize-operation-identifier-generation"></a>Dostosowywanie generowania identyfikatora operacji
Swashbuckle generuje identyfikatory operacji programu Swagger, łącząc nazwy kontrolera i nazwy metody. Ten wzorzec tworzy problem, jeśli masz wiele przeciążenia metody: Swashbuckle generuje operacji zduplikowane identyfikatory, która jest nieprawidłowa JSON programu Swagger.

Na przykład następujący kod kontrolera powoduje, że pakiet Swashbuckle do generowania trzech identyfikatorów operacji Contact_Get.

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

Problem można rozwiązać ręcznie, zapewniając metody unikatowe nazwy, takie jak wymienione poniżej w tym przykładzie:

* Get
* GetById
* GetPage

Alternatywą jest rozszerzenie Swashbuckle, aby automatycznie wygenerować operacji unikatowych identyfikatorów.

W poniższej procedurze pokazano sposób dostosowywania Swashbuckle za pomocą *SwaggerConfig.cs* pliku, który jest dołączony do projektu przez szablon projektu Visual Studio Preview aplikacji interfejsu API.  Można również dostosować Swashbuckle w projekcie interfejsu API sieci Web skonfigurowana dla wdrażania aplikacji interfejsu API.

1. Utworzenie niestandardowego `IOperationFilter` implementacji 
   
    `IOperationFilter` Interfejs zapewnia punkt rozszerzeń dla użytkowników Swashbuckle, którzy chcą dostosować różnych aspektów procesu metadanych struktury Swagger. Poniższy kod przedstawia jedną z metod zmiany zachowania operacji identyfikatora generacji. Kod dołącza nazwy parametrów na nazwę identyfikatora operacji.  
   
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
2. W *App_Start\SwaggerConfig.cs* plików, należy wywołać `OperationFilter` metodę, aby spowodować, że pakiet Swashbuckle do używania nowych `IOperationFilter` implementacji.
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    *SwaggerConfig.cs* plików, które są przenoszone przez pakiet Swashbuckle NuGet zawiera wiele przykładów poza komentarzem punkty rozszerzeń. Dodatkowe komentarze nie są wyświetlane tutaj. 
   
    Po wprowadzeniu tej zmiany z `IOperationFilter` implementacji jest używana i powoduje, że operacji unikatowych identyfikatorów do wygenerowania.
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a>Zezwalaj na kody odpowiedzi innych niż 200
Domyślnie pakiet Swashbuckle zakłada, że odpowiedź 200 protokołu HTTP (OK) *tylko* prawnie odpowiedzi z metody interfejsu API sieci Web. W niektórych przypadkach warto zwrócić innych kodów odpowiedzi bez powodowania klienta zgłosić wyjątek.  Na przykład w poniższym kodzie interfejsu API sieci Web przedstawiono scenariusz, w którym ma czy klient akceptuje 200 lub 404 jako prawidłowy odpowiedzi.

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

W tym scenariuszu Swagger, który Swashbuckle generuje domyślnie określa tylko jeden uzasadnionych kod stanu HTTP, 200 protokołu HTTP.

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

Ponieważ program Visual Studio korzysta definicji interfejsu API programu Swagger do generowania kodu klienta, tworzy kod klienta, który zgłasza wyjątek dla odpowiedzi innych niż 200 protokołu HTTP. Poniższy kod jest w kliencie C# wygenerowany dla tej próbki metody interfejsu API sieci Web.

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

Pakiet Swashbuckle oferuje dwa sposoby dostosowywania Lista oczekiwanych kody odpowiedzi HTTP, które generuje za pomocą komentarze XML lub `SwaggerResponse` atrybutu. Ten atrybut jest łatwiejsze, ale tylko jest dostępna w Swashbuckle 5.1.5 lub nowszej. Szablon aplikacji interfejsu API w wersji zapoznawczej nowy projekt w programie Visual Studio 2013 zawiera Swashbuckle wersji 5.0.0, więc jeśli używany szablon i nie chcesz zaktualizować pakiet Swashbuckle, jedyną opcją jest użycie komentarze XML. 

### <a name="customize-expected-response-codes-using-xml-comments"></a>Dostosowywanie kodów odpowiedzi oczekiwanego przy użyciu komentarze XML
Ta metoda umożliwia określenie kody odpowiedzi, jeśli pakiet Swashbuckle wersja jest wcześniejsza niż 5.1.5.

1. Najpierw dodaj komentarze dokumentacji XML za pośrednictwem metody, które chcesz określić kody odpowiedzi HTTP. Pobieranie próbki interfejsu API sieci Web akcji pokazanym powyżej i zastosowanie dokumentacji XML do niej spowoduje kodu, jak w następującym przykładzie. 
   
        /// <summary>
        /// Returns the specified contact.
        /// </summary>
        /// <param name="id">The ID of the contact.</param>
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
2. Dodaj instrukcje w *SwaggerConfig.cs* pliku przekierować Swashbuckle, aby użyć pliku XML dokumentacji pliku.
   
   * Otwórz *SwaggerConfig.cs* i utworzyć metodę na *SwaggerConfig* klasę, aby określić ścieżkę do pliku dokumentacji XML. 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * Przewiń w dół *SwaggerConfig.cs* pliku, aż zostanie wyświetlony wiersz poza komentarzem kodu przypominającą zrzut poniżej ekranu. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * Usuń komentarz linii, aby włączyć komentarze XML przetwarzania podczas generowania struktury Swagger. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. Aby wygenerować plik dokumentacji XML, przejdź do właściwości projektu i Włącz pliku dokumentacji XML, jak pokazano na poniższym zrzucie ekranu. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

Po wykonaniu tych kroków JSON programu Swagger generowane przez pakiet Swashbuckle, zostaną one zastosowane kody odpowiedzi HTTP, które zostały określone w komentarzach XML. Na poniższym zrzucie ekranu przedstawiono ten nowy ładunek JSON. 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

Korzystając z programu Visual Studio można ponownie wygenerować kod klienta dla interfejsu API REST, kodu C# akceptuje kodów stanu HTTP OK i nie można odnaleźć bez podnoszenia wyjątek, dzięki czemu kod odbierającą do podejmowania decyzji o sposobie obsługi zwracany rekord skontaktuj się z wartości null. 

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

Kod używany w tej prezentacji można znaleźć w [to repozytorium GitHub](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse). Wraz z interfejsu API sieci Web projektu oznaczonych komentarze dokumentacji XML jest projekt aplikacji konsoli, który zawiera wygenerowanego klienta dla tego interfejsu API. 

### <a name="customize-expected-response-codes-using-the-swaggerresponse-attribute"></a>Dostosowywanie kodów odpowiedzi oczekiwanego przy użyciu atrybutu SwaggerResponse
[SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) atrybutu jest dostępna w Swashbuckle 5.1.5 lub nowszej. W przypadku, gdy w projekcie jest zainstalowana starsza wersja tej sekcji rozpoczyna się od wyjaśniający, jak zaktualizować pakiet Swashbuckle NuGet, dzięki czemu można użyć tego atrybutu.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt interfejsu API sieci Web i kliknij przycisk **Zarządzaj pakietami NuGet**. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. Kliknij przycisk *aktualizacji* znajdujący się obok *Swashbuckle* pakietu NuGet. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. Dodaj *SwaggerResponse* atrybuty do metod akcji interfejsu API sieci Web, dla których chcesz określić prawidłowy kody odpowiedzi HTTP. 
   
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
4. Dodaj `using` instrukcji dla atrybutu przestrzeni nazw:
   
        using Swashbuckle.Swagger.Annotations;
5. Przejdź do */swagger/docs/v1* adres URL projektu i różnych kodów odpowiedzi HTTP będzie widoczny w formacie JSON programu Swagger. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

Kod używany w tej prezentacji można znaleźć w [to repozytorium GitHub](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes). Wraz z projektu interfejsu API sieci Web ozdobione *SwaggerResponse* atrybut jest projekt aplikacji konsoli, który zawiera wygenerowanego klienta dla tego interfejsu API. 

## <a name="next-steps"></a>Następne kroki
W tym artykule pokazuje, jak dostosować Swashbuckle generuje identyfikatorów operacji i kody prawidłowej odpowiedzi. Aby uzyskać więcej informacji, zobacz [Swashbuckle w serwisie GitHub](https://github.com/domaindrivendev/Swashbuckle).

