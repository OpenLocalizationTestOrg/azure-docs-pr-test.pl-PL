---
title: "aaaException zarządzania — narzędzie modelowania zagrożeń Microsoft - Azure | Dokumentacja firmy Microsoft"
description: "środki zaradcze w przypadku zagrożeń w hello narzędzie modelowania zagrożeń"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 247096c10deeca94ebb9b19df7ba60e442ca1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-exception-management--mitigations"></a><span data-ttu-id="362df-103">Ramka zabezpieczeń: Zarządzanie wyjątkami | Środki zaradcze</span><span class="sxs-lookup"><span data-stu-id="362df-103">Security Frame: Exception Management | Mitigations</span></span> 
| <span data-ttu-id="362df-104">Produktów i usług</span><span class="sxs-lookup"><span data-stu-id="362df-104">Product/Service</span></span> | <span data-ttu-id="362df-105">Artykuł</span><span class="sxs-lookup"><span data-stu-id="362df-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="362df-106">**WCF**</span><span class="sxs-lookup"><span data-stu-id="362df-106">**WCF**</span></span> | <ul><li>[<span data-ttu-id="362df-107">Usługi WCF - nie zawiera węzła serviceDebug w pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="362df-107">WCF- Do not include serviceDebug node in configuration file</span></span>](#servicedebug)</li><li>[<span data-ttu-id="362df-108">Usługi WCF - nie zawiera węzła serviceMetadata w pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="362df-108">WCF- Do not include serviceMetadata node in configuration file</span></span>](#servicemetadata)</li></ul> |
| <span data-ttu-id="362df-109">**Interfejs API sieci Web**</span><span class="sxs-lookup"><span data-stu-id="362df-109">**Web API**</span></span> | <ul><li>[<span data-ttu-id="362df-110">Upewnij się, że odpowiednich wyjątków odbywa się w interfejsie API sieci Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="362df-110">Ensure that proper exception handling is done in ASP.NET Web API </span></span>](#exception)</li></ul> |
| <span data-ttu-id="362df-111">**Aplikacja sieci Web**</span><span class="sxs-lookup"><span data-stu-id="362df-111">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="362df-112">Nie ujawniaj szczegóły zabezpieczeń w komunikatach o błędach</span><span class="sxs-lookup"><span data-stu-id="362df-112">Do not expose security details in error messages </span></span>](#messages)</li><li>[<span data-ttu-id="362df-113">Implementowanie obsługi strony błędów domyślne</span><span class="sxs-lookup"><span data-stu-id="362df-113">Implement Default error handling page </span></span>](#default)</li><li>[<span data-ttu-id="362df-114">Ustaw tooRetail metody wdrażania w usługach IIS</span><span class="sxs-lookup"><span data-stu-id="362df-114">Set Deployment Method tooRetail in IIS</span></span>](#deployment)</li><li>[<span data-ttu-id="362df-115">Wyjątki powinna zakończyć się niepowodzeniem bezpiecznie</span><span class="sxs-lookup"><span data-stu-id="362df-115">Exceptions should fail safely</span></span>](#fail)</li></ul> |

## <span data-ttu-id="362df-116"><a id="servicedebug"></a>Usługi WCF - nie zawiera węzła serviceDebug w pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="362df-116"><a id="servicedebug"></a>WCF- Do not include serviceDebug node in configuration file</span></span>

| <span data-ttu-id="362df-117">Tytuł</span><span class="sxs-lookup"><span data-stu-id="362df-117">Title</span></span>                   | <span data-ttu-id="362df-118">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="362df-118">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="362df-119">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="362df-119">**Component**</span></span>               | <span data-ttu-id="362df-120">WCF</span><span class="sxs-lookup"><span data-stu-id="362df-120">WCF</span></span> | 
| <span data-ttu-id="362df-121">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="362df-121">**SDL Phase**</span></span>               | <span data-ttu-id="362df-122">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="362df-122">Build</span></span> |  
| <span data-ttu-id="362df-123">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="362df-123">**Applicable Technologies**</span></span> | <span data-ttu-id="362df-124">Ogólny, NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="362df-124">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="362df-125">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="362df-125">**Attributes**</span></span>              | <span data-ttu-id="362df-126">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="362df-126">N/A</span></span>  |
| <span data-ttu-id="362df-127">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="362df-127">**References**</span></span>              | <span data-ttu-id="362df-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [uzyskania zawartości Królestwo](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="362df-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="362df-129">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="362df-129">**Steps**</span></span> | <span data-ttu-id="362df-130">Usług Windows Communication Framework (WCF) może być skonfigurowany tooexpose informacji o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="362df-130">Windows Communication Framework (WCF) services can be configured tooexpose debugging information.</span></span> <span data-ttu-id="362df-131">Debugowanie informacji nie powinna być używana w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="362df-131">Debug information should not be used in production environments.</span></span> <span data-ttu-id="362df-132">Witaj `<serviceDebug>` tagów Określa, czy funkcja informacji o debugowaniu hello jest włączone dla usługi WCF.</span><span class="sxs-lookup"><span data-stu-id="362df-132">hello `<serviceDebug>` tag defines whether hello debug information feature is enabled for a WCF service.</span></span> <span data-ttu-id="362df-133">Jeśli includeExceptionDetailInFaults atrybutu hello ustawiono tootrue, informacje o wyjątku z aplikacji hello zostanie zwrócony tooclients.</span><span class="sxs-lookup"><span data-stu-id="362df-133">If hello attribute includeExceptionDetailInFaults is set tootrue, exception information from hello application will be returned tooclients.</span></span> <span data-ttu-id="362df-134">Osoby atakujące mogą korzystać z hello dodatkowe informacje, które będą mogli z debugowania dane wyjściowe toomount ataków ukierunkowanych hello framework, bazy danych lub innych zasobów używanych przez aplikację hello.</span><span class="sxs-lookup"><span data-stu-id="362df-134">Attackers can leverage hello additional information they gain from debugging output toomount attacks targeted on hello framework, database, or other resources used by hello application.</span></span> |

### <a name="example"></a><span data-ttu-id="362df-135">Przykład</span><span class="sxs-lookup"><span data-stu-id="362df-135">Example</span></span>
<span data-ttu-id="362df-136">Witaj następujący plik konfiguracji zawiera hello `<serviceDebug>` tagu:</span><span class="sxs-lookup"><span data-stu-id="362df-136">hello following configuration file includes hello `<serviceDebug>` tag:</span></span> 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
<span data-ttu-id="362df-137">Wyłącz informacji o debugowaniu w usłudze hello.</span><span class="sxs-lookup"><span data-stu-id="362df-137">Disable debugging information in hello service.</span></span> <span data-ttu-id="362df-138">Można to zrobić przez usunięcie hello `<serviceDebug>` tagu z pliku konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="362df-138">This can be accomplished by removing hello `<serviceDebug>` tag from your application's configuration file.</span></span> 

## <span data-ttu-id="362df-139"><a id="servicemetadata"></a>Usługi WCF - nie zawiera węzła serviceMetadata w pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="362df-139"><a id="servicemetadata"></a>WCF- Do not include serviceMetadata node in configuration file</span></span>

| <span data-ttu-id="362df-140">Tytuł</span><span class="sxs-lookup"><span data-stu-id="362df-140">Title</span></span>                   | <span data-ttu-id="362df-141">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="362df-141">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="362df-142">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="362df-142">**Component**</span></span>               | <span data-ttu-id="362df-143">WCF</span><span class="sxs-lookup"><span data-stu-id="362df-143">WCF</span></span> | 
| <span data-ttu-id="362df-144">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="362df-144">**SDL Phase**</span></span>               | <span data-ttu-id="362df-145">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="362df-145">Build</span></span> |  
| <span data-ttu-id="362df-146">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="362df-146">**Applicable Technologies**</span></span> | <span data-ttu-id="362df-147">Ogólny</span><span class="sxs-lookup"><span data-stu-id="362df-147">Generic</span></span> |
| <span data-ttu-id="362df-148">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="362df-148">**Attributes**</span></span>              | <span data-ttu-id="362df-149">Ogólny, NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="362df-149">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="362df-150">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="362df-150">**References**</span></span>              | <span data-ttu-id="362df-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [uzyskania zawartości Królestwo](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="362df-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="362df-152">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="362df-152">**Steps**</span></span> | <span data-ttu-id="362df-153">Publicznie udostępnianie informacji na temat usługi umożliwia atakującym cenny wgląd w sposób może wykorzystać hello usługi.</span><span class="sxs-lookup"><span data-stu-id="362df-153">Publicly exposing information about a service can provide attackers with valuable insight into how they might exploit hello service.</span></span> <span data-ttu-id="362df-154">Witaj `<serviceMetadata>` tag włącza funkcję publikowania hello metadanych.</span><span class="sxs-lookup"><span data-stu-id="362df-154">hello `<serviceMetadata>` tag enables hello metadata publishing feature.</span></span> <span data-ttu-id="362df-155">Metadane usługi mogą zawierać poufne informacje, które nie powinny być publicznie dostępne.</span><span class="sxs-lookup"><span data-stu-id="362df-155">Service metadata could contain sensitive information that should not be publicly accessible.</span></span> <span data-ttu-id="362df-156">Co najmniej umożliwiają tylko przez zaufanych użytkowników tooaccess hello metadanych i upewnij się, że niepotrzebnych informacji nie jest uwidaczniana.</span><span class="sxs-lookup"><span data-stu-id="362df-156">At a minimum, only allow trusted users tooaccess hello metadata and ensure that unnecessary information is not exposed.</span></span> <span data-ttu-id="362df-157">Jeszcze lepiej całkowicie wyłączyć hello możliwości toopublish metadanych.</span><span class="sxs-lookup"><span data-stu-id="362df-157">Better yet, entirely disable hello ability toopublish metadata.</span></span> <span data-ttu-id="362df-158">Bezpieczne konfiguracji usługi WCF nie będą zawierać hello `<serviceMetadata>` tagu.</span><span class="sxs-lookup"><span data-stu-id="362df-158">A safe WCF configuration will not contain hello `<serviceMetadata>` tag.</span></span> |

## <span data-ttu-id="362df-159"><a id="exception"></a>Upewnij się, że odpowiednich wyjątków odbywa się w interfejsie API sieci Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="362df-159"><a id="exception"></a>Ensure that proper exception handling is done in ASP.NET Web API</span></span>

| <span data-ttu-id="362df-160">Tytuł</span><span class="sxs-lookup"><span data-stu-id="362df-160">Title</span></span>                   | <span data-ttu-id="362df-161">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="362df-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="362df-162">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="362df-162">**Component**</span></span>               | <span data-ttu-id="362df-163">Interfejs API sieci Web</span><span class="sxs-lookup"><span data-stu-id="362df-163">Web API</span></span> | 
| <span data-ttu-id="362df-164">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="362df-164">**SDL Phase**</span></span>               | <span data-ttu-id="362df-165">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="362df-165">Build</span></span> |  
| <span data-ttu-id="362df-166">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="362df-166">**Applicable Technologies**</span></span> | <span data-ttu-id="362df-167">MVC 5, 6 MVC</span><span class="sxs-lookup"><span data-stu-id="362df-167">MVC 5, MVC 6</span></span> |
| <span data-ttu-id="362df-168">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="362df-168">**Attributes**</span></span>              | <span data-ttu-id="362df-169">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="362df-169">N/A</span></span>  |
| <span data-ttu-id="362df-170">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="362df-170">**References**</span></span>              | <span data-ttu-id="362df-171">[Obsługa wyjątków w ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [modelu weryfikacji w składniku ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span><span class="sxs-lookup"><span data-stu-id="362df-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span></span> |
| <span data-ttu-id="362df-172">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="362df-172">**Steps**</span></span> | <span data-ttu-id="362df-173">Domyślnie większość nieprzechwyconych wyjątków w interfejsie API sieci Web platformy ASP.NET są przetłumaczyć z kodem stanu odpowiedzi HTTP`500, Internal Server Error`</span><span class="sxs-lookup"><span data-stu-id="362df-173">By default, most uncaught exceptions in ASP.NET Web API are translated into an HTTP response with status code `500, Internal Server Error`</span></span>|

### <a name="example"></a><span data-ttu-id="362df-174">Przykład</span><span class="sxs-lookup"><span data-stu-id="362df-174">Example</span></span>
<span data-ttu-id="362df-175">Kod stanu hello toocontrol zwrócony przez hello interfejsu API, `HttpResponseException` można w sposób przedstawiony poniżej:</span><span class="sxs-lookup"><span data-stu-id="362df-175">toocontrol hello status code returned by hello API, `HttpResponseException` can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        throw new HttpResponseException(HttpStatusCode.NotFound);
    }
    return item;
}
```

### <a name="example"></a><span data-ttu-id="362df-176">Przykład</span><span class="sxs-lookup"><span data-stu-id="362df-176">Example</span></span>
<span data-ttu-id="362df-177">Dla dalszego kontrolę nad hello wyjątek odpowiedzi, hello `HttpResponseMessage` klasa może być używana, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="362df-177">For further control on hello exception response, hello `HttpResponseMessage` class can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        var resp = new HttpResponseMessage(HttpStatusCode.NotFound)
        {
            Content = new StringContent(string.Format("No product with ID = {0}", id)),
            ReasonPhrase = "Product ID Not Found"
        }
        throw new HttpResponseException(resp);
    }
    return item;
}
```
<span data-ttu-id="362df-178">toocatch nieobsługiwane wyjątki, które nie są typu hello `HttpResponseException`, filtry wyjątków mogą być używane.</span><span class="sxs-lookup"><span data-stu-id="362df-178">toocatch unhandled exceptions that are not of hello type `HttpResponseException`, Exception Filters can be used.</span></span> <span data-ttu-id="362df-179">Filtry wyjątków zaimplementować hello `System.Web.Http.Filters.IExceptionFilter` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="362df-179">Exception filters implement hello `System.Web.Http.Filters.IExceptionFilter` interface.</span></span> <span data-ttu-id="362df-180">Witaj najprostszy sposób toowrite filtra wyjątku jest tooderive z hello `System.Web.Http.Filters.ExceptionFilterAttribute` klasy i przesłonić metodę OnException hello.</span><span class="sxs-lookup"><span data-stu-id="362df-180">hello simplest way toowrite an exception filter is tooderive from hello `System.Web.Http.Filters.ExceptionFilterAttribute` class and override hello OnException method.</span></span> 

### <a name="example"></a><span data-ttu-id="362df-181">Przykład</span><span class="sxs-lookup"><span data-stu-id="362df-181">Example</span></span>
<span data-ttu-id="362df-182">Oto filtr, który konwertuje `NotImplementedException` wyjątków w kodzie stanu HTTP `501, Not Implemented`:</span><span class="sxs-lookup"><span data-stu-id="362df-182">Here is a filter that converts `NotImplementedException` exceptions into HTTP status code `501, Not Implemented`:</span></span> 
```C#
namespace ProductStore.Filters
{
    using System;
    using System.Net;
    using System.Net.Http;
    using System.Web.Http.Filters;

    public class NotImplExceptionFilterAttribute : ExceptionFilterAttribute 
    {
        public override void OnException(HttpActionExecutedContext context)
        {
            if (context.Exception is NotImplementedException)
            {
                context.Response = new HttpResponseMessage(HttpStatusCode.NotImplemented);
            }
        }
    }
}
```

<span data-ttu-id="362df-183">Istnieje kilka sposobów tooregister filtru wyjątków interfejsu API sieci Web:</span><span class="sxs-lookup"><span data-stu-id="362df-183">There are several ways tooregister a Web API exception filter:</span></span>
- <span data-ttu-id="362df-184">Przez akcję</span><span class="sxs-lookup"><span data-stu-id="362df-184">By action</span></span>
- <span data-ttu-id="362df-185">Kontroler</span><span class="sxs-lookup"><span data-stu-id="362df-185">By controller</span></span>
- <span data-ttu-id="362df-186">Globalny</span><span class="sxs-lookup"><span data-stu-id="362df-186">Globally</span></span>

### <a name="example"></a><span data-ttu-id="362df-187">Przykład</span><span class="sxs-lookup"><span data-stu-id="362df-187">Example</span></span>
<span data-ttu-id="362df-188">Witaj tooapply Filtruj tooa określonej akcji, Dodaj filtr hello jako akcja toohello atrybutu:</span><span class="sxs-lookup"><span data-stu-id="362df-188">tooapply hello filter tooa specific action, add hello filter as an attribute toohello action:</span></span> 
```C#
public class ProductsController : ApiController
{
    [NotImplExceptionFilter]
    public Contact GetContact(int id)
    {
        throw new NotImplementedException("This method is not implemented");
    }
}
```
### <a name="example"></a><span data-ttu-id="362df-189">Przykład</span><span class="sxs-lookup"><span data-stu-id="362df-189">Example</span></span>
<span data-ttu-id="362df-190">tooapply hello filtru tooall działania hello `controller`, Dodaj filtr hello jako atrybut toohello `controller` klasy:</span><span class="sxs-lookup"><span data-stu-id="362df-190">tooapply hello filter tooall of hello actions on a `controller`, add hello filter as an attribute toohello `controller` class:</span></span> 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a><span data-ttu-id="362df-191">Przykład</span><span class="sxs-lookup"><span data-stu-id="362df-191">Example</span></span>
<span data-ttu-id="362df-192">tooapply hello filtrować globalnie tooall kontrolerów interfejsu API sieci Web, dodać wystąpienia toohello filtru hello `GlobalConfiguration.Configuration.Filters` kolekcji.</span><span class="sxs-lookup"><span data-stu-id="362df-192">tooapply hello filter globally tooall Web API controllers, add an instance of hello filter toohello `GlobalConfiguration.Configuration.Filters` collection.</span></span> <span data-ttu-id="362df-193">Filtry wyjątków w tej kolekcji stosowanie akcji kontrolera interfejsu API sieci Web tooany.</span><span class="sxs-lookup"><span data-stu-id="362df-193">Exception filters in this collection apply tooany Web API controller action.</span></span> 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a><span data-ttu-id="362df-194">Przykład</span><span class="sxs-lookup"><span data-stu-id="362df-194">Example</span></span>
<span data-ttu-id="362df-195">Weryfikacja modelu hello stan modelu mogą być przekazywane metody tooCreateErrorResponse, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="362df-195">For model validation, hello model state can be passed tooCreateErrorResponse method as shown below:</span></span> 
```C#
public HttpResponseMessage PostProduct(Product item)
{
    if (!ModelState.IsValid)
    {
        return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
    }
    // Implementation not shown...
}
```

<span data-ttu-id="362df-196">Łącza hello wyboru w sekcji odwołań hello, aby uzyskać więcej informacji o obsługę wyjątkowych i sprawdzania poprawności modelu w interfejsie API sieci Web ASP.Net</span><span class="sxs-lookup"><span data-stu-id="362df-196">Check hello links in hello references section for additional details about exceptional handling and model validation in ASP.Net Web API</span></span> 

## <span data-ttu-id="362df-197"><a id="messages"></a>Nie ujawniaj szczegóły zabezpieczeń w komunikatach o błędach</span><span class="sxs-lookup"><span data-stu-id="362df-197"><a id="messages"></a>Do not expose security details in error messages</span></span>

| <span data-ttu-id="362df-198">Tytuł</span><span class="sxs-lookup"><span data-stu-id="362df-198">Title</span></span>                   | <span data-ttu-id="362df-199">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="362df-199">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="362df-200">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="362df-200">**Component**</span></span>               | <span data-ttu-id="362df-201">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="362df-201">Web Application</span></span> | 
| <span data-ttu-id="362df-202">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="362df-202">**SDL Phase**</span></span>               | <span data-ttu-id="362df-203">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="362df-203">Build</span></span> |  
| <span data-ttu-id="362df-204">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="362df-204">**Applicable Technologies**</span></span> | <span data-ttu-id="362df-205">Ogólny</span><span class="sxs-lookup"><span data-stu-id="362df-205">Generic</span></span> |
| <span data-ttu-id="362df-206">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="362df-206">**Attributes**</span></span>              | <span data-ttu-id="362df-207">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="362df-207">N/A</span></span>  |
| <span data-ttu-id="362df-208">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="362df-208">**References**</span></span>              | <span data-ttu-id="362df-209">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="362df-209">N/A</span></span>  |
| <span data-ttu-id="362df-210">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="362df-210">**Steps**</span></span> | <p><span data-ttu-id="362df-211">Ogólne komunikaty o błędach są dostarczane bezpośrednio toohello użytkownika bez uwzględniania aplikacji poufnych danych.</span><span class="sxs-lookup"><span data-stu-id="362df-211">Generic error messages are provided directly toohello user without including sensitive application data.</span></span> <span data-ttu-id="362df-212">Przykłady danych poufnych:</span><span class="sxs-lookup"><span data-stu-id="362df-212">Examples of sensitive data include:</span></span></p><ul><li><span data-ttu-id="362df-213">Nazwy serwerów</span><span class="sxs-lookup"><span data-stu-id="362df-213">Server names</span></span></li><li><span data-ttu-id="362df-214">Parametry połączeń</span><span class="sxs-lookup"><span data-stu-id="362df-214">Connection strings</span></span></li><li><span data-ttu-id="362df-215">Nazwy użytkowników</span><span class="sxs-lookup"><span data-stu-id="362df-215">Usernames</span></span></li><li><span data-ttu-id="362df-216">Hasła</span><span class="sxs-lookup"><span data-stu-id="362df-216">Passwords</span></span></li><li><span data-ttu-id="362df-217">Procedury SQL</span><span class="sxs-lookup"><span data-stu-id="362df-217">SQL procedures</span></span></li><li><span data-ttu-id="362df-218">Szczegóły błędów SQL dynamiczne</span><span class="sxs-lookup"><span data-stu-id="362df-218">Details of dynamic SQL failures</span></span></li><li><span data-ttu-id="362df-219">Ślad stosu i wiersze kodu</span><span class="sxs-lookup"><span data-stu-id="362df-219">Stack trace and lines of code</span></span></li><li><span data-ttu-id="362df-220">Zmiennych przechowywanych w pamięci</span><span class="sxs-lookup"><span data-stu-id="362df-220">Variables stored in memory</span></span></li><li><span data-ttu-id="362df-221">Dysk i folder lokalizacji</span><span class="sxs-lookup"><span data-stu-id="362df-221">Drive and folder locations</span></span></li><li><span data-ttu-id="362df-222">Punkty instalacji aplikacji</span><span class="sxs-lookup"><span data-stu-id="362df-222">Application install points</span></span></li><li><span data-ttu-id="362df-223">Ustawienia konfiguracji hosta</span><span class="sxs-lookup"><span data-stu-id="362df-223">Host configuration settings</span></span></li><li><span data-ttu-id="362df-224">Inne szczegóły aplikacja wewnętrzna</span><span class="sxs-lookup"><span data-stu-id="362df-224">Other internal application details</span></span></li></ul><p><span data-ttu-id="362df-225">Generują pułapki wszystkich błędów w aplikacji i zapewnianie ogólne komunikaty o błędach, a także włączenie błędy niestandardowe w ramach usług IIS pomaga zapobiegać ujawnienie informacji.</span><span class="sxs-lookup"><span data-stu-id="362df-225">Trapping all errors within an application and providing generic error messages, as well as enabling custom errors within IIS will help prevent information disclosure.</span></span> <span data-ttu-id="362df-226">Bazy danych programu SQL Server i .NET obsługi wyjątków, między inny błąd obsługi architektury, są szczególnie pełne i bardzo przydatne tooa złośliwy użytkownik profilowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="362df-226">SQL Server database and .NET Exception handling, among other error handling architectures, are especially verbose and extremely useful tooa malicious user profiling your application.</span></span> <span data-ttu-id="362df-227">Czy nie bezpośrednio hello wyświetlana zawartość klasę pochodną klasy wyjątków .NET hello i sprawdź, czy mają odpowiednie wyjątków, dzięki czemu wystąpił nieoczekiwany wyjątek nie jest przypadkowo wywoływane bezpośrednio toohello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="362df-227">Do not directly display hello contents of a class derived from hello .NET Exception class, and ensure that you have proper exception handling so that an unexpected exception isn't inadvertently raised directly toohello user.</span></span></p><ul><li><span data-ttu-id="362df-228">Podaj ogólne komunikaty o błędach bezpośrednio toohello użytkownika, który abstrakcyjnej zadań bezpośrednio w wiadomości powitania błąd wyjątku/konkretne szczegółowe informacje</span><span class="sxs-lookup"><span data-stu-id="362df-228">Provide generic error messages directly toohello user that abstract away specific details found directly in hello exception/error message</span></span></li><li><span data-ttu-id="362df-229">Wyświetlana zawartość hello wyjątku .NET bezpośrednio klasa toohello użytkownika</span><span class="sxs-lookup"><span data-stu-id="362df-229">Do not display hello contents of a .NET exception class directly toohello user</span></span></li><li><span data-ttu-id="362df-230">Pułapki wszystkie komunikaty o błędach i w razie potrzeby o hello użytkownika za pośrednictwem błąd rodzajowy komunikat wysłany toohello aplikacji klienta</span><span class="sxs-lookup"><span data-stu-id="362df-230">Trap all error messages and if appropriate inform hello user via a generic error message sent toohello application client</span></span></li><li><span data-ttu-id="362df-231">Nie ujawniaj hello zawartość klasy wyjątku hello bezpośrednio toohello użytkowników, szczególnie hello wartością zwracaną z `.ToString()`, lub wartości hello hello właściwości wiadomości i ślad stosu.</span><span class="sxs-lookup"><span data-stu-id="362df-231">Do not expose hello contents of hello Exception class directly toohello user, especially hello return value from `.ToString()`, or hello values of hello Message or StackTrace properties.</span></span> <span data-ttu-id="362df-232">Bezpiecznego logowania tych informacji i wyświetlić więcej nieszkodliwe użytkownika toohello wiadomości</span><span class="sxs-lookup"><span data-stu-id="362df-232">Securely log this information and display a more innocuous message toohello user</span></span></li></ul>|

## <span data-ttu-id="362df-233"><a id="default"></a>Implementowanie obsługi strony błędów domyślne</span><span class="sxs-lookup"><span data-stu-id="362df-233"><a id="default"></a>Implement Default error handling page</span></span>

| <span data-ttu-id="362df-234">Tytuł</span><span class="sxs-lookup"><span data-stu-id="362df-234">Title</span></span>                   | <span data-ttu-id="362df-235">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="362df-235">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="362df-236">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="362df-236">**Component**</span></span>               | <span data-ttu-id="362df-237">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="362df-237">Web Application</span></span> | 
| <span data-ttu-id="362df-238">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="362df-238">**SDL Phase**</span></span>               | <span data-ttu-id="362df-239">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="362df-239">Build</span></span> |  
| <span data-ttu-id="362df-240">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="362df-240">**Applicable Technologies**</span></span> | <span data-ttu-id="362df-241">Ogólny</span><span class="sxs-lookup"><span data-stu-id="362df-241">Generic</span></span> |
| <span data-ttu-id="362df-242">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="362df-242">**Attributes**</span></span>              | <span data-ttu-id="362df-243">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="362df-243">N/A</span></span>  |
| <span data-ttu-id="362df-244">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="362df-244">**References**</span></span>              | <span data-ttu-id="362df-245">[Edytuj okno dialogowe ustawień stron błędów ASP.NET](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="362df-245">[Edit ASP.NET Error Pages Settings Dialog Box](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span></span> |
| <span data-ttu-id="362df-246">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="362df-246">**Steps**</span></span> | <p><span data-ttu-id="362df-247">Aplikacja ASP.NET nie powiedzie się i powoduje, że wystąpił wewnętrzny błąd serwera HTTP/1.x 500 lub Konfiguracja funkcji, (na przykład Filtrowanie żądań) zapobiega wyświetlaniu strony, zostanie wygenerowany komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="362df-247">When an ASP.NET application fails and causes an HTTP/1.x 500 Internal Server Error, or a feature configuration (such as Request Filtering) prevents a page from being displayed, an error message will be generated.</span></span> <span data-ttu-id="362df-248">Administratorzy mogą wybrać, czy aplikacja hello powinien być wyświetlany, przyjazny komunikat toohello klienta, szczegółowe informacje o błędzie komunikat toohello klienta lub tylko toolocalhost komunikat szczegółowe informacje o błędzie.</span><span class="sxs-lookup"><span data-stu-id="362df-248">Administrators can choose whether or not hello application should display a friendly message toohello client, detailed error message toohello client, or detailed error message toolocalhost only.</span></span> <span data-ttu-id="362df-249">Witaj <customErrors> znacznika w pliku web.config hello ma trzy tryby:</span><span class="sxs-lookup"><span data-stu-id="362df-249">hello <customErrors> tag in hello web.config has three modes:</span></span></p><ul><li><span data-ttu-id="362df-250">**Na:** Określa, czy błędy niestandardowe są włączone.</span><span class="sxs-lookup"><span data-stu-id="362df-250">**On:** Specifies that custom errors are enabled.</span></span> <span data-ttu-id="362df-251">Jeśli zostanie określony bez atrybutu defaultRedirect, użytkownicy widzą błąd ogólny.</span><span class="sxs-lookup"><span data-stu-id="362df-251">If no defaultRedirect attribute is specified, users see a generic error.</span></span> <span data-ttu-id="362df-252">błędy niestandardowe Hello są wyświetlane toohello klienci zdalni i toohello hosta lokalnego</span><span class="sxs-lookup"><span data-stu-id="362df-252">hello custom errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="362df-253">**OFF:** Określa, czy błędy niestandardowe są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="362df-253">**Off:** Specifies that custom errors are disabled.</span></span> <span data-ttu-id="362df-254">Witaj szczegółowe błędy programu ASP.NET są wyświetlane toohello klienci zdalni i toohello hosta lokalnego</span><span class="sxs-lookup"><span data-stu-id="362df-254">hello detailed ASP.NET errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="362df-255">**RemoteOnly:** Określa, czy błędy niestandardowe są widoczne tylko toohello klienci zdalni i że błędy programu ASP.NET są pokazywane toohello hosta lokalnego.</span><span class="sxs-lookup"><span data-stu-id="362df-255">**RemoteOnly:** Specifies that custom errors are shown only toohello remote clients, and that ASP.NET errors are shown toohello local host.</span></span> <span data-ttu-id="362df-256">Jest to wartość domyślna hello</span><span class="sxs-lookup"><span data-stu-id="362df-256">This is hello default value</span></span></li></ul><p><span data-ttu-id="362df-257">Otwórz hello `web.config` dla witryny aplikacji hello i upewnij się, że hello tag ma `<customErrors mode="RemoteOnly" />` lub `<customErrors mode="On" />` zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="362df-257">Open hello `web.config` file for hello application/site and ensure that hello tag has either `<customErrors mode="RemoteOnly" />` or `<customErrors mode="On" />` defined.</span></span></p>|

## <span data-ttu-id="362df-258"><a id="deployment"></a>Ustaw tooRetail metody wdrażania w usługach IIS</span><span class="sxs-lookup"><span data-stu-id="362df-258"><a id="deployment"></a>Set Deployment Method tooRetail in IIS</span></span>

| <span data-ttu-id="362df-259">Tytuł</span><span class="sxs-lookup"><span data-stu-id="362df-259">Title</span></span>                   | <span data-ttu-id="362df-260">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="362df-260">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="362df-261">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="362df-261">**Component**</span></span>               | <span data-ttu-id="362df-262">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="362df-262">Web Application</span></span> | 
| <span data-ttu-id="362df-263">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="362df-263">**SDL Phase**</span></span>               | <span data-ttu-id="362df-264">Wdrożenie</span><span class="sxs-lookup"><span data-stu-id="362df-264">Deployment</span></span> |  
| <span data-ttu-id="362df-265">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="362df-265">**Applicable Technologies**</span></span> | <span data-ttu-id="362df-266">Ogólny</span><span class="sxs-lookup"><span data-stu-id="362df-266">Generic</span></span> |
| <span data-ttu-id="362df-267">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="362df-267">**Attributes**</span></span>              | <span data-ttu-id="362df-268">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="362df-268">N/A</span></span>  |
| <span data-ttu-id="362df-269">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="362df-269">**References**</span></span>              | <span data-ttu-id="362df-270">[wdrożenie — Element (schemat ustawień programu ASP.NET)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="362df-270">[deployment Element (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span></span> |
| <span data-ttu-id="362df-271">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="362df-271">**Steps**</span></span> | <p><span data-ttu-id="362df-272">Witaj `<deployment retail>` przełącznik jest przeznaczony dla systemów produkcyjnych serwerów usług IIS.</span><span class="sxs-lookup"><span data-stu-id="362df-272">hello `<deployment retail>` switch is intended for use by production IIS servers.</span></span> <span data-ttu-id="362df-273">Ten parametr jest toohelp używane aplikacje o najlepszej wydajności możliwe hello i najniższe możliwe informacji zabezpieczających wycieków wyłączając hello danych wyjściowych śledzenia toogenerate możliwości aplikacji na stronie wyłączenie toodisplay możliwości hello szczegóły błędu Użytkownicy tooend wiadomości i wyłączanie hello debugowania przełącznika.</span><span class="sxs-lookup"><span data-stu-id="362df-273">This switch is used toohelp applications run with hello best possible performance and least possible security information leakages by disabling hello application's ability toogenerate trace output on a page, disabling hello ability toodisplay detailed error messages tooend users, and disabling hello debug switch.</span></span></p><p><span data-ttu-id="362df-274">Często, przełączniki i opcje, które są ukierunkowane developer, takie jak nie powiodło się żądanie śledzenia i debugowania, są włączane podczas opracowywania active.</span><span class="sxs-lookup"><span data-stu-id="362df-274">Often times, switches and options that are developer-focused, such as failed request tracing and debugging, are enabled during active development.</span></span> <span data-ttu-id="362df-275">Zaleca się, że metoda wdrażania hello na dowolnym serwerze produkcyjnym można ustawić tooretail.</span><span class="sxs-lookup"><span data-stu-id="362df-275">It is recommended that hello deployment method on any production server be set tooretail.</span></span> <span data-ttu-id="362df-276">Otwórz plik machine.config hello i upewnij się, że `<deployment retail="true" />` pozostanie wartość tootrue.</span><span class="sxs-lookup"><span data-stu-id="362df-276">open hello machine.config file and ensure that `<deployment retail="true" />` remains set tootrue.</span></span></p>|

## <span data-ttu-id="362df-277"><a id="fail"></a>Wyjątki powinna zakończyć się niepowodzeniem bezpiecznie</span><span class="sxs-lookup"><span data-stu-id="362df-277"><a id="fail"></a>Exceptions should fail safely</span></span>

| <span data-ttu-id="362df-278">Tytuł</span><span class="sxs-lookup"><span data-stu-id="362df-278">Title</span></span>                   | <span data-ttu-id="362df-279">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="362df-279">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="362df-280">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="362df-280">**Component**</span></span>               | <span data-ttu-id="362df-281">Aplikacja sieci Web</span><span class="sxs-lookup"><span data-stu-id="362df-281">Web Application</span></span> | 
| <span data-ttu-id="362df-282">**Faza SDL**</span><span class="sxs-lookup"><span data-stu-id="362df-282">**SDL Phase**</span></span>               | <span data-ttu-id="362df-283">Kompilacja</span><span class="sxs-lookup"><span data-stu-id="362df-283">Build</span></span> |  
| <span data-ttu-id="362df-284">**Zastosowanie technologii**</span><span class="sxs-lookup"><span data-stu-id="362df-284">**Applicable Technologies**</span></span> | <span data-ttu-id="362df-285">Ogólny</span><span class="sxs-lookup"><span data-stu-id="362df-285">Generic</span></span> |
| <span data-ttu-id="362df-286">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="362df-286">**Attributes**</span></span>              | <span data-ttu-id="362df-287">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="362df-287">N/A</span></span>  |
| <span data-ttu-id="362df-288">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="362df-288">**References**</span></span>              | [<span data-ttu-id="362df-289">Niepowodzenie bezpiecznego</span><span class="sxs-lookup"><span data-stu-id="362df-289">Fail securely</span></span>](https://www.owasp.org/index.php/Fail_securely) |
| <span data-ttu-id="362df-290">**Kroki**</span><span class="sxs-lookup"><span data-stu-id="362df-290">**Steps**</span></span> | <span data-ttu-id="362df-291">Aplikacja powinna zakończyć się niepowodzeniem bezpiecznie.</span><span class="sxs-lookup"><span data-stu-id="362df-291">Application should fail safely.</span></span> <span data-ttu-id="362df-292">Dowolnej metody, która zwraca wartość logiczną, oparte na następuje pewnych decyzji, powinien mieć dokładnie utworzyć bloku wyjątków.</span><span class="sxs-lookup"><span data-stu-id="362df-292">Any method that returns a Boolean value, based on which certain decision is made, should have exception block carefully created.</span></span> <span data-ttu-id="362df-293">Istnieje wiele błędów logicznych powodu pełzanie problemy zabezpieczeń toowhich w po bloku wyjątków hello napisano zaniedbali.</span><span class="sxs-lookup"><span data-stu-id="362df-293">There are lot of logical errors due toowhich security issues creep in, when hello exception block is written carelessly.</span></span>|

### <a name="example"></a><span data-ttu-id="362df-294">Przykład</span><span class="sxs-lookup"><span data-stu-id="362df-294">Example</span></span>
```C#
        public static bool ValidateDomain(string pathToValidate, Uri currentUrl)
        {
            try
            {
                if (!string.IsNullOrWhiteSpace(pathToValidate))
                {
                    var domain = RetrieveDomain(currentUrl);
                    var replyPath = new Uri(pathToValidate);
                    var replyDomain = RetrieveDomain(replyPath);

                    if (string.Compare(domain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                    {
                        //// Adding additional check tooenable CMS urls if they are not hosted on same domain.
                        if (!string.IsNullOrWhiteSpace(Utilities.CmsBase))
                        {
                            var cmsDomain = RetrieveDomain(new Uri(Utilities.Base.Trim()));
                            if (string.Compare(cmDomain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                            {
                                return false;
                            }
                            else
                            {
                                return true;
                            }
                        }

                        return false;
                    }
                }

                return true;
            }
            catch (UriFormatException ex)
            {
                LogHelper.LogException("Utilities:ValidateDomain", ex);
                return true;
            }
        }
```
<span data-ttu-id="362df-295">Hello powyżej metoda zawsze zwraca wartość PRAWDA, jeśli wystąpi wyjątek.</span><span class="sxs-lookup"><span data-stu-id="362df-295">hello above method will always return True, if some exception happens.</span></span> <span data-ttu-id="362df-296">Jeśli użytkownik końcowy hello zawiera źle sformułowany adres URL, który hello względem przeglądarki, ale hello `Uri()` Konstruktor nie, to spowoduje zgłoszenie wyjątku i ofiara hello zostaną wykonane toohello prawidłowe, ale źle sformułowany adres URL.</span><span class="sxs-lookup"><span data-stu-id="362df-296">If hello end user provides a malformed URL, that hello browser respects, but hello `Uri()` constructor doesn't, this will throw an exception, and hello victim will be taken toohello valid but malformed URL.</span></span> 
