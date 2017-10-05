---
title: "Zaawansowane zasady zarządzania interfejsu API platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej na temat zaawansowanych zasad dostępne do użycia w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 8a13348b-7856-428f-8e35-9e4273d94323
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0c65ac74316421a0258f01143baa25ffecb5be3b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="api-management-advanced-policies"></a><span data-ttu-id="72563-103">Zarządzanie interfejsami API zaawansowane zasady</span><span class="sxs-lookup"><span data-stu-id="72563-103">API Management advanced policies</span></span>
<span data-ttu-id="72563-104">W tym temacie znajdują się informacje na następujące zasady usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="72563-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="72563-105">Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="72563-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="72563-106"><a name="AdvancedPolicies"></a>Zaawansowane zasady</span><span class="sxs-lookup"><span data-stu-id="72563-106"><a name="AdvancedPolicies"></a> Advanced policies</span></span>  
  
-   <span data-ttu-id="72563-107">[Przepływ kontroli](api-management-advanced-policies.md#choose) — warunkowo stosuje deklaracji zasad, na podstawie wyników oceny Boolean [wyrażenia](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="72563-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the results of the evaluation of Boolean [expressions](api-management-policy-expressions.md).</span></span>  
  
-   <span data-ttu-id="72563-108">[Przekazanie żądania](#ForwardRequest) -przekazuje żądanie do usługi zaplecza.</span><span class="sxs-lookup"><span data-stu-id="72563-108">[Forward request](#ForwardRequest) - Forwards the request to the backend service.</span></span>

-   <span data-ttu-id="72563-109">[Ogranicz współbieżności](#LimitConcurrency) — uniemożliwia ujęta zasady wykonania przez więcej niż określoną liczbę żądań w czasie.</span><span class="sxs-lookup"><span data-stu-id="72563-109">[Limit concurrency](#LimitConcurrency) - Prevents enclosed policies from executing by more than the specified number of requests at a time.</span></span>
  
-   <span data-ttu-id="72563-110">[Dziennika do Centrum zdarzeń](#log-to-eventhub) — wysyła komunikaty w określonym formacie do Centrum zdarzeń zdefiniowanych przez podmiot rejestratora.</span><span class="sxs-lookup"><span data-stu-id="72563-110">[Log to Event Hub](#log-to-eventhub) - Sends messages in the specified format to an Event Hub defined by a Logger entity.</span></span> 

-   <span data-ttu-id="72563-111">[Mock odpowiedzi](#mock-response) -przerwań potoku wykonywania i zwraca odpowiedź mocked bezpośrednio do obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="72563-111">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly to the caller.</span></span>
  
-   <span data-ttu-id="72563-112">[Spróbuj ponownie](#Retry) -ponowi próbę wykonania instrukcji objętego zasad, jeśli i do momentu spełnienia warunku.</span><span class="sxs-lookup"><span data-stu-id="72563-112">[Retry](#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="72563-113">Wykonanie Powtórz w określonych odstępach czasu, a także do określonej liczba ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="72563-113">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>  
  
-   <span data-ttu-id="72563-114">[Odpowiedź zwrócona](#ReturnResponse) -przerwań potoku wykonywania i zwraca określoną odpowiedzią bezpośrednio do obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="72563-114">[Return response](#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span> 
  
-   <span data-ttu-id="72563-115">[Wyślij żądanie jednokierunkowej](#SendOneWayRequest) — wysyła żądanie pod określony adres URL bez oczekiwania na odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="72563-115">[Send one way request](#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>  
  
-   <span data-ttu-id="72563-116">[Wyślij żądanie](#SendRequest) — wysyła żądanie do określonego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="72563-116">[Send request](#SendRequest) - Sends a request to the specified URL.</span></span>  

-   <span data-ttu-id="72563-117">[Ustaw serwer proxy HTTP](#SetHttpProxy) — zezwala na żądania trasy przekazywane za pośrednictwem serwera proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="72563-117">[Set HTTP proxy](#SetHttpProxy) - Allows you to route forwarded requests via an HTTP proxy.</span></span>  

-   <span data-ttu-id="72563-118">[Ustawia metodę żądania](#SetRequestMethod) — umożliwia zmianę metody HTTP dla żądania.</span><span class="sxs-lookup"><span data-stu-id="72563-118">[Set request method](#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>  
  
-   <span data-ttu-id="72563-119">[Ustaw kod stanu](#SetStatus) — zmienia kod stanu HTTP do określonej wartości.</span><span class="sxs-lookup"><span data-stu-id="72563-119">[Set status code](#SetStatus) - Changes the HTTP status code to the specified value.</span></span>  
  
-   <span data-ttu-id="72563-120">[Ustaw zmienną](api-management-advanced-policies.md#set-variable) -będzie się powtarzał wartości w nazwanym [kontekstu](api-management-policy-expressions.md#ContextVariables) zmiennej nowsze dostępu.</span><span class="sxs-lookup"><span data-stu-id="72563-120">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span></span>  

-   <span data-ttu-id="72563-121">[Śledzenia](#Trace) -dodaje ciąg do [inspektora interfejsu API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="72563-121">[Trace](#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
-   <span data-ttu-id="72563-122">[Poczekaj](#Wait) -oczekuje dla ujęta [żądanie wysłania](api-management-advanced-policies.md#SendRequest), [pobrać wartości z pamięci podręcznej](api-management-caching-policies.md#GetFromCacheByKey), lub [sterowania przepływem](api-management-advanced-policies.md#choose) zasad, aby ukończyć przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="72563-122">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span></span>  
  
##  <span data-ttu-id="72563-123"><a name="choose"></a>Przepływ sterowania</span><span class="sxs-lookup"><span data-stu-id="72563-123"><a name="choose"></a> Control flow</span></span>  
 <span data-ttu-id="72563-124">`choose` Zasad stosuje objętego zasady w oparciu o wyniki obliczania wyrażeń logicznych, podobnie jak w przypadku to inaczej lub przełącznika instrukcje tworzenia w języku programowania.</span><span class="sxs-lookup"><span data-stu-id="72563-124">The `choose` policy applies enclosed policy statements based on the outcome of evaluation of Boolean expressions, similar to an if-then-else or a switch construct in a programming language.</span></span>  
  
###  <span data-ttu-id="72563-125"><a name="ChoosePolicyStatement"></a>Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="72563-125"><a name="ChoosePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements to be applied if the above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements to be applied if the above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements to be applied if none of the above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 <span data-ttu-id="72563-126">Zasady kontroli przepływu musi zawierać co najmniej jeden `<when/>` elementu.</span><span class="sxs-lookup"><span data-stu-id="72563-126">The control flow policy must contain at least one `<when/>` element.</span></span> <span data-ttu-id="72563-127">`<otherwise/>` Element jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="72563-127">The `<otherwise/>` element is optional.</span></span> <span data-ttu-id="72563-128">Warunki w `<when/>` elementy są oceniane w kolejności ich wyglądu w zasadzie.</span><span class="sxs-lookup"><span data-stu-id="72563-128">Conditions in `<when/>` elements are evaluated in order of their appearance within the policy.</span></span> <span data-ttu-id="72563-129">Instrukcji zasad ujętą w nawiasy klamrowe pierwszy `<when/>` element z równą atrybut warunku `true` zostaną zastosowane.</span><span class="sxs-lookup"><span data-stu-id="72563-129">Policy statement(s) enclosed within the first `<when/>` element with condition attribute equals `true` will be applied.</span></span> <span data-ttu-id="72563-130">Zasady ujętą w nawiasy klamrowe `<otherwise/>` elementu, jeśli jest obecny, zostaną zastosowane, jeśli wszystkie z `<when/>` są atrybuty warunku elementu `false`.</span><span class="sxs-lookup"><span data-stu-id="72563-130">Policies enclosed within the `<otherwise/>` element, if present, will be applied if all of the `<when/>` element condition attributes are `false`.</span></span>  
  
### <a name="examples"></a><span data-ttu-id="72563-131">Przykłady</span><span class="sxs-lookup"><span data-stu-id="72563-131">Examples</span></span>  
  
####  <span data-ttu-id="72563-132"><a name="ChooseExample"></a>Przykład</span><span class="sxs-lookup"><span data-stu-id="72563-132"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="72563-133">W poniższym przykładzie pokazano [set-variable](api-management-advanced-policies.md#set-variable) zasad i dwie zasady przepływu sterowania.</span><span class="sxs-lookup"><span data-stu-id="72563-133">The following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span></span>  
  
 <span data-ttu-id="72563-134">Ustaw zasady zmiennej znajduje się w sekcji dla ruchu przychodzącego i tworzy `isMobile` logiczna [kontekstu](api-management-policy-expressions.md#ContextVariables) zmiennej, która ma ustawioną wartość true, jeśli `User-Agent` tekst zawiera nagłówek żądania `iPad` lub `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="72563-134">The set variable policy is in the inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span></span>  
  
 <span data-ttu-id="72563-135">Pierwszy zasad przepływu sterowania jest również w sekcji dla ruchu przychodzącego i warunkowo stosuje się jeden z dwóch [ustawić parametr ciągu zapytania](api-management-transformation-policies.md#SetQueryStringParameter) zasad w zależności od wartości `isMobile` zmiennej kontekstu.</span><span class="sxs-lookup"><span data-stu-id="72563-135">The first control flow policy is also in the inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on the value of the `isMobile` context variable.</span></span>  
  
 <span data-ttu-id="72563-136">Drugie zasady przepływu sterowania znajduje się w sekcji wychodzących i warunkowo stosuje [XML Konwertuj do formatu JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) zasad podczas `isMobile` ma ustawioną wartość `true`.</span><span class="sxs-lookup"><span data-stu-id="72563-136">The second control flow policy is in the outbound section and conditionally applies the [Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set to `true`.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <set-variable name="isMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
        <base />  
        <choose>  
            <when condition="@(context.Variables.GetValueOrDefault<bool>("isMobile"))">  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>true</value>  
                </set-query-parameter>  
            </when>  
            <otherwise>  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>false</value>  
                </set-query-parameter>  
            </otherwise>  
        </choose>  
    </inbound>  
    <outbound>  
        <base />  
        <choose>  
            <when condition="@(context.GetValueOrDefault<bool>("isMobile"))">  
                <xml-to-json kind="direct" apply="always" consider-accept-header="false"/>  
            </when>  
        </choose>  
    </outbound>  
</policies>  
```  
  
#### <a name="example"></a><span data-ttu-id="72563-137">Przykład</span><span class="sxs-lookup"><span data-stu-id="72563-137">Example</span></span>  
 <span data-ttu-id="72563-138">W tym przykładzie pokazano, jak wykonać filtrowanie zawartości przez usunięcie elementów danych z odpowiedzi otrzymał od usługi wewnętrznej bazy danych, korzystając z `Starter` produktu.</span><span class="sxs-lookup"><span data-stu-id="72563-138">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span></span> <span data-ttu-id="72563-139">Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybkie przewijanie do przodu do 34:30.</span><span class="sxs-lookup"><span data-stu-id="72563-139">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span></span> <span data-ttu-id="72563-140">Rozpocznij od 31:50 wyświetlić przegląd [ciemny niebo prognozy interfejsu API](https://developer.forecast.io/) używane na potrzeby tego pokazu.</span><span class="sxs-lookup"><span data-stu-id="72563-140">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into the outbound section to remove a number of data elements from the response received from the backend service based on the name of the api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  
  
### <a name="elements"></a><span data-ttu-id="72563-141">Elementy</span><span class="sxs-lookup"><span data-stu-id="72563-141">Elements</span></span>  
  
|<span data-ttu-id="72563-142">Element</span><span class="sxs-lookup"><span data-stu-id="72563-142">Element</span></span>|<span data-ttu-id="72563-143">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-143">Description</span></span>|<span data-ttu-id="72563-144">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-144">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="72563-145">Wybierz pozycję</span><span class="sxs-lookup"><span data-stu-id="72563-145">choose</span></span>|<span data-ttu-id="72563-146">Element główny.</span><span class="sxs-lookup"><span data-stu-id="72563-146">Root element.</span></span>|<span data-ttu-id="72563-147">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-147">Yes</span></span>|  
|<span data-ttu-id="72563-148">Kiedy</span><span class="sxs-lookup"><span data-stu-id="72563-148">when</span></span>|<span data-ttu-id="72563-149">Warunek, którego chcesz użyć dla `if` lub `ifelse` części `choose` zasad.</span><span class="sxs-lookup"><span data-stu-id="72563-149">The condition to use for the `if` or `ifelse` parts of the `choose` policy.</span></span> <span data-ttu-id="72563-150">Jeśli `choose` zasad ma wiele `when` sekcje są oceniane po kolei.</span><span class="sxs-lookup"><span data-stu-id="72563-150">If the `choose` policy has multiple `when` sections, they are evaluated sequentially.</span></span> <span data-ttu-id="72563-151">Raz `condition` z o tym, kiedy element daje w wyniku `true`, nie musisz `when` oceny warunków.</span><span class="sxs-lookup"><span data-stu-id="72563-151">Once the `condition` of a when element evaluates to `true`, no further `when` conditions are evaluated.</span></span>|<span data-ttu-id="72563-152">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-152">Yes</span></span>|  
|<span data-ttu-id="72563-153">w przeciwnym razie</span><span class="sxs-lookup"><span data-stu-id="72563-153">otherwise</span></span>|<span data-ttu-id="72563-154">Zawiera fragment zasad do użycia, jeśli żadna z `when` warunki obliczać `true`.</span><span class="sxs-lookup"><span data-stu-id="72563-154">Contains the policy snippet to be used if none of the `when` conditions evaluate to `true`.</span></span>|<span data-ttu-id="72563-155">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-155">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72563-156">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="72563-156">Attributes</span></span>  
  
|<span data-ttu-id="72563-157">Atrybut</span><span class="sxs-lookup"><span data-stu-id="72563-157">Attribute</span></span>|<span data-ttu-id="72563-158">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-158">Description</span></span>|<span data-ttu-id="72563-159">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-159">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="72563-160">warunek = "wyrażenie warunkowe &#124; Wartość logiczna stała"</span><span class="sxs-lookup"><span data-stu-id="72563-160">condition="Boolean expression &#124; Boolean constant"</span></span>|<span data-ttu-id="72563-161">Wyrażenia logicznego lub stała się obliczone, gdy zawierający `when` oceny deklaracji zasad.</span><span class="sxs-lookup"><span data-stu-id="72563-161">The Boolean expression or constant to evaluated when the containing `when` policy statement is evaluated.</span></span>|<span data-ttu-id="72563-162">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-162">Yes</span></span>|  
  
###  <span data-ttu-id="72563-163"><a name="ChooseUsage"></a>Użycie</span><span class="sxs-lookup"><span data-stu-id="72563-163"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="72563-164">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72563-164">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72563-165">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="72563-165">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="72563-166">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="72563-166">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="72563-167"><a name="ForwardRequest"></a>Przekazanie żądania</span><span class="sxs-lookup"><span data-stu-id="72563-167"><a name="ForwardRequest"></a> Forward request</span></span>  
 <span data-ttu-id="72563-168">`forward-request` Zasad przesyła żądanie przychodzące do usługi zaplecza, określony w żądaniu [kontekstu](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="72563-168">The `forward-request` policy forwards the incoming request to the backend service specified in the request [context](api-management-policy-expressions.md#ContextVariables).</span></span> <span data-ttu-id="72563-169">Adres URL usługi wewnętrznej bazy danych jest określony w interfejsie API [ustawienia](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) i można zmienić za pomocą [Ustaw usługę zaplecza](api-management-transformation-policies.md) zasad.</span><span class="sxs-lookup"><span data-stu-id="72563-169">The backend service URL is specified in the API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using the [set backend service](api-management-transformation-policies.md) policy.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="72563-170">Usuwanie wyników tej zasady w żądaniu nie są przekazywane do wewnętrznej bazy danych usługi i zasady w sekcji wychodzące są oceniane natychmiast po pomyślnym zakończeniu zasady w sekcji dla ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="72563-170">Removing this policy results in the request not being forwarded to the backend service and the policies in the outbound section are evaluated immediately upon the successful completion of the policies in the inbound section.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="72563-171">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="72563-171">Policy statement</span></span>  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a><span data-ttu-id="72563-172">Przykłady</span><span class="sxs-lookup"><span data-stu-id="72563-172">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="72563-173">Przykład</span><span class="sxs-lookup"><span data-stu-id="72563-173">Example</span></span>  
 <span data-ttu-id="72563-174">Następujące zasady na poziomie interfejsu API przekazuje wszystkie żądania do usługi wewnętrznej bazy danych z limit czasu 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="72563-174">The following API level policy forwards all requests to the backend service with a timeout interval of 60 seconds.</span></span>  
  
```xml  
<!-- api level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="60"/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="72563-175">Przykład</span><span class="sxs-lookup"><span data-stu-id="72563-175">Example</span></span>  
 <span data-ttu-id="72563-176">Używa tej zasady na poziomie operacji `base` element dziedziczenie zasad wewnętrznej bazy danych z nadrzędnym zakresie poziomu interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="72563-176">This operation level policy uses the `base` element to inherit the backend policy from the parent API level scope.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <base/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="72563-177">Przykład</span><span class="sxs-lookup"><span data-stu-id="72563-177">Example</span></span>  
 <span data-ttu-id="72563-178">Ta operacja zasady na poziomie jawnie przekazuje wszystkie żądania do usługi zaplecza z limitem czasu 120 i nie dziedziczy nadrzędnego zasad poziomu zaplecza interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="72563-178">This operation level policy explicitly forwards all requests to the backend service with a timeout of 120 and does not inherit the parent API level backend policy.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note the absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="72563-179">Przykład</span><span class="sxs-lookup"><span data-stu-id="72563-179">Example</span></span>  
 <span data-ttu-id="72563-180">Zasady na poziomie tej operacji nie przekazuje żądania do usługi zaplecza.</span><span class="sxs-lookup"><span data-stu-id="72563-180">This operation level policy does not forward requests to the backend service.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding to backend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="72563-181">Elementy</span><span class="sxs-lookup"><span data-stu-id="72563-181">Elements</span></span>  
  
|<span data-ttu-id="72563-182">Element</span><span class="sxs-lookup"><span data-stu-id="72563-182">Element</span></span>|<span data-ttu-id="72563-183">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-183">Description</span></span>|<span data-ttu-id="72563-184">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-184">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="72563-185">żądanie do przodu</span><span class="sxs-lookup"><span data-stu-id="72563-185">forward-request</span></span>|<span data-ttu-id="72563-186">Element główny.</span><span class="sxs-lookup"><span data-stu-id="72563-186">Root element.</span></span>|<span data-ttu-id="72563-187">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-187">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72563-188">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="72563-188">Attributes</span></span>  
  
|<span data-ttu-id="72563-189">Atrybut</span><span class="sxs-lookup"><span data-stu-id="72563-189">Attribute</span></span>|<span data-ttu-id="72563-190">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-190">Description</span></span>|<span data-ttu-id="72563-191">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-191">Required</span></span>|<span data-ttu-id="72563-192">Domyślne</span><span class="sxs-lookup"><span data-stu-id="72563-192">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="72563-193">limit czasu = "int"</span><span class="sxs-lookup"><span data-stu-id="72563-193">timeout="integer"</span></span>|<span data-ttu-id="72563-194">Interwał limitu czasu w sekundach przed wywołaniem usługi wewnętrznej bazy danych nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="72563-194">The timeout interval in seconds before the call to the backend service fails.</span></span>|<span data-ttu-id="72563-195">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-195">No</span></span>|<span data-ttu-id="72563-196">Brak limitu czasu</span><span class="sxs-lookup"><span data-stu-id="72563-196">No timeout</span></span>|  
|<span data-ttu-id="72563-197">Wykonaj przekierowania = "true &#124; false"</span><span class="sxs-lookup"><span data-stu-id="72563-197">follow-redirects="true &#124; false"</span></span>|<span data-ttu-id="72563-198">Określa, czy przekierowania z usługi wewnętrznej bazy danych są następuje bramy lub zwracany do obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="72563-198">Specifies whether redirects from the backend service are followed by the gateway or returned to the caller.</span></span>|<span data-ttu-id="72563-199">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-199">No</span></span>|<span data-ttu-id="72563-200">wartość false</span><span class="sxs-lookup"><span data-stu-id="72563-200">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="72563-201">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="72563-201">Usage</span></span>  
 <span data-ttu-id="72563-202">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72563-202">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72563-203">**Sekcje zasad:** wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="72563-203">**Policy sections:** backend</span></span>  
  
-   <span data-ttu-id="72563-204">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="72563-204">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="72563-205"><a name="LimitConcurrency"></a>Limit współbieżności</span><span class="sxs-lookup"><span data-stu-id="72563-205"><a name="LimitConcurrency"></a> Limit concurrency</span></span>  
 <span data-ttu-id="72563-206">`limit-concurrency` Zasad uniemożliwia objętego zasad wykonywania przez więcej niż określoną liczbę żądań w danym momencie.</span><span class="sxs-lookup"><span data-stu-id="72563-206">The `limit-concurrency` policy prevents enclosed policies from executing by more than the specified number of requests at a given time.</span></span> <span data-ttu-id="72563-207">Po przekroczeniu progu, nowe żądania są dodawane do kolejki, do kolejki maksymalną długość.</span><span class="sxs-lookup"><span data-stu-id="72563-207">Upon exceeding the threshold, new requests are added to a queue, until the maximum queue length is achieved.</span></span> <span data-ttu-id="72563-208">Po wyczerpania kolejki nowe żądania nie powiedzie się natychmiast.</span><span class="sxs-lookup"><span data-stu-id="72563-208">Upon queue exhaustion, new requests will fail immediately.</span></span>
  
###  <span data-ttu-id="72563-209"><a name="LimitConcurrencyStatement"></a>Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="72563-209"><a name="LimitConcurrencyStatement"></a> Policy statement</span></span>  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a><span data-ttu-id="72563-210">Przykłady</span><span class="sxs-lookup"><span data-stu-id="72563-210">Examples</span></span>  
  
####  <span data-ttu-id="72563-211"><a name="ChooseExample"></a>Przykład</span><span class="sxs-lookup"><span data-stu-id="72563-211"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="72563-212">W poniższym przykładzie pokazano sposób ograniczyć liczbę przekazywany do wewnętrznej bazy danych na podstawie wartości zmiennej kontekstu żądania.</span><span class="sxs-lookup"><span data-stu-id="72563-212">The following example demonstrates how to limit number of requests forwarded to a backend based on the value of a context variable.</span></span>
 
```xml  
<policies>
  <inbound>…</inbound>
  <backend>
    <limit-concurrency key="@((string)context.Variables["connectionId"])" max-count="3" timeout="60">
      <forward-request timeout="120"/>
    <limit-concurrency/>
  </backend>
  <outbound>…</outbound>
</policies>
```

### <a name="elements"></a><span data-ttu-id="72563-213">Elementy</span><span class="sxs-lookup"><span data-stu-id="72563-213">Elements</span></span>  
  
|<span data-ttu-id="72563-214">Element</span><span class="sxs-lookup"><span data-stu-id="72563-214">Element</span></span>|<span data-ttu-id="72563-215">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-215">Description</span></span>|<span data-ttu-id="72563-216">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-216">Required</span></span>|  
|-------------|-----------------|--------------|    
|<span data-ttu-id="72563-217">limit współbieżności</span><span class="sxs-lookup"><span data-stu-id="72563-217">limit-concurrency</span></span>|<span data-ttu-id="72563-218">Element główny.</span><span class="sxs-lookup"><span data-stu-id="72563-218">Root element.</span></span>|<span data-ttu-id="72563-219">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72563-220">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="72563-220">Attributes</span></span>  
  
|<span data-ttu-id="72563-221">Atrybut</span><span class="sxs-lookup"><span data-stu-id="72563-221">Attribute</span></span>|<span data-ttu-id="72563-222">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-222">Description</span></span>|<span data-ttu-id="72563-223">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-223">Required</span></span>|<span data-ttu-id="72563-224">Domyślne</span><span class="sxs-lookup"><span data-stu-id="72563-224">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="72563-225">key</span><span class="sxs-lookup"><span data-stu-id="72563-225">key</span></span>|<span data-ttu-id="72563-226">Ciąg.</span><span class="sxs-lookup"><span data-stu-id="72563-226">A string.</span></span> <span data-ttu-id="72563-227">Wyrażenie jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="72563-227">Expression allowed.</span></span> <span data-ttu-id="72563-228">Określa zakres współbieżności.</span><span class="sxs-lookup"><span data-stu-id="72563-228">Specifies the concurrency scope.</span></span> <span data-ttu-id="72563-229">Może być współużytkowane przez wiele zasad.</span><span class="sxs-lookup"><span data-stu-id="72563-229">Can be shared by multiple policies.</span></span>|<span data-ttu-id="72563-230">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-230">Yes</span></span>|<span data-ttu-id="72563-231">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="72563-231">N/A</span></span>|  
|<span data-ttu-id="72563-232">Maksymalna liczba</span><span class="sxs-lookup"><span data-stu-id="72563-232">max-count</span></span>|<span data-ttu-id="72563-233">Liczba całkowita.</span><span class="sxs-lookup"><span data-stu-id="72563-233">An integer.</span></span> <span data-ttu-id="72563-234">Określa maksymalną liczbę żądań, które mogą wprowadzać zasady.</span><span class="sxs-lookup"><span data-stu-id="72563-234">Specifies a maximum number of requests that are allowed to enter the policy.</span></span>|<span data-ttu-id="72563-235">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-235">Yes</span></span>|<span data-ttu-id="72563-236">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="72563-236">N/A</span></span>|  
|<span data-ttu-id="72563-237">Limit czasu</span><span class="sxs-lookup"><span data-stu-id="72563-237">timeout</span></span>|<span data-ttu-id="72563-238">Liczba całkowita.</span><span class="sxs-lookup"><span data-stu-id="72563-238">An integer.</span></span> <span data-ttu-id="72563-239">Wyrażenie jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="72563-239">Expression allowed.</span></span> <span data-ttu-id="72563-240">Określa liczbę sekund, żądanie powinno czekać z wprowadź zakres przed niepowodzeniem z "403 zbyt wiele żądań"</span><span class="sxs-lookup"><span data-stu-id="72563-240">Specifies the number of seconds a request should wait to enter a scope before failing with "403 Too Many Requests"</span></span>|<span data-ttu-id="72563-241">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-241">No</span></span>|<span data-ttu-id="72563-242">Infinity</span><span class="sxs-lookup"><span data-stu-id="72563-242">Infinity</span></span>|  
|<span data-ttu-id="72563-243">Maksymalna kolejki</span><span class="sxs-lookup"><span data-stu-id="72563-243">max-queue-length</span></span>|<span data-ttu-id="72563-244">Liczba całkowita.</span><span class="sxs-lookup"><span data-stu-id="72563-244">An integer.</span></span> <span data-ttu-id="72563-245">Wyrażenie jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="72563-245">Expression allowed.</span></span> <span data-ttu-id="72563-246">Określa długość maksymalna kolejki.</span><span class="sxs-lookup"><span data-stu-id="72563-246">Specifies the maximum queue length.</span></span> <span data-ttu-id="72563-247">Żądań przychodzących w trakcie wprowadzania tych zasad, zostanie zakończony z "403 zbyt wiele żądań" natychmiast po wyczerpaniu kolejki.</span><span class="sxs-lookup"><span data-stu-id="72563-247">Incoming requests trying to enter this policy will be terminated with “403 Too Many Requests” immediately when the queue is exhausted.</span></span>|<span data-ttu-id="72563-248">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-248">No</span></span>|<span data-ttu-id="72563-249">Infinity</span><span class="sxs-lookup"><span data-stu-id="72563-249">Infinity</span></span>|  
  
###  <span data-ttu-id="72563-250"><a name="ChooseUsage"></a>Użycie</span><span class="sxs-lookup"><span data-stu-id="72563-250"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="72563-251">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72563-251">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72563-252">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="72563-252">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="72563-253">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="72563-253">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="72563-254"><a name="log-to-eventhub"></a>Dziennika do Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="72563-254"><a name="log-to-eventhub"></a> Log to Event Hub</span></span>  
 <span data-ttu-id="72563-255">`log-to-eventhub` Zasad wysyła komunikaty w określonym formacie do Centrum zdarzeń zdefiniowanych przez podmiot rejestratora.</span><span class="sxs-lookup"><span data-stu-id="72563-255">The `log-to-eventhub` policy sends messages in the specified format to an Event Hub defined by a Logger entity.</span></span> <span data-ttu-id="72563-256">Jak jego nazwa wskazuje, zasady są używane do zapisywania wybrane informacje kontekstu żądania lub odpowiedzi do analizy w trybie online lub offline.</span><span class="sxs-lookup"><span data-stu-id="72563-256">As its name implies, the policy is used for saving selected request or response context information for online or offline analysis.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="72563-257">Przewodnik krok po kroku dotyczące konfigurowania Centrum zdarzeń i rejestrowania zdarzeń dla [jak mają być rejestrowane zdarzenia zarządzanie interfejsami API w usłudze Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="72563-257">For a step-by-step guide on configuring an event hub and logging events, see [How to log API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="72563-258">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="72563-258">Policy statement</span></span>  
  
```xml  
<log-to-eventhub logger-id="id of the logger entity" partition-id="index of the partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string to be logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a><span data-ttu-id="72563-259">Przykład</span><span class="sxs-lookup"><span data-stu-id="72563-259">Example</span></span>  
 <span data-ttu-id="72563-260">Dowolny ciąg może służyć jako wartość mają być rejestrowane w usłudze Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="72563-260">Any string can be used as the value to be logged in Event Hubs.</span></span> <span data-ttu-id="72563-261">W tym przykładzie daty i godziny, nazwa usługi wdrożenia, identyfikator żądania, adresu ip oraz nazwy operacji dla wszystkich połączeń przychodzących, które są rejestrowane w Centrum zdarzeń zarejestrowany rejestratora `contoso-logger` identyfikator.</span><span class="sxs-lookup"><span data-stu-id="72563-261">In this example the date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged to the event hub Logger registered with the `contoso-logger` id.</span></span>  
  
```xml  
<policies>  
  <inbound>  
    <log-to-eventhub logger-id ='contoso-logger'>  
      @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name) )   
    </log-to-eventhub>  
  </inbound>  
  <outbound>          
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="72563-262">Elementy</span><span class="sxs-lookup"><span data-stu-id="72563-262">Elements</span></span>  
  
|<span data-ttu-id="72563-263">Element</span><span class="sxs-lookup"><span data-stu-id="72563-263">Element</span></span>|<span data-ttu-id="72563-264">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-264">Description</span></span>|<span data-ttu-id="72563-265">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-265">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="72563-266">dziennika do Centrum eventhub</span><span class="sxs-lookup"><span data-stu-id="72563-266">log-to-eventhub</span></span>|<span data-ttu-id="72563-267">Element główny.</span><span class="sxs-lookup"><span data-stu-id="72563-267">Root element.</span></span> <span data-ttu-id="72563-268">Wartość tego elementu jest ciąg do logowania się do Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="72563-268">The value of this element is the string to log to your event hub.</span></span>|<span data-ttu-id="72563-269">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-269">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72563-270">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="72563-270">Attributes</span></span>  
  
|<span data-ttu-id="72563-271">Atrybut</span><span class="sxs-lookup"><span data-stu-id="72563-271">Attribute</span></span>|<span data-ttu-id="72563-272">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-272">Description</span></span>|<span data-ttu-id="72563-273">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-273">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="72563-274">identyfikator rejestratora</span><span class="sxs-lookup"><span data-stu-id="72563-274">logger-id</span></span>|<span data-ttu-id="72563-275">Identyfikator rejestratora zarejestrowana przy użyciu usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="72563-275">The id of the Logger registered with your API Management service.</span></span>|<span data-ttu-id="72563-276">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-276">Yes</span></span>|  
|<span data-ttu-id="72563-277">Identyfikator partycji</span><span class="sxs-lookup"><span data-stu-id="72563-277">partition-id</span></span>|<span data-ttu-id="72563-278">Określa indeks partycji, którego wysyłane są wiadomości.</span><span class="sxs-lookup"><span data-stu-id="72563-278">Specifies the index of the partition where messages are sent.</span></span>|<span data-ttu-id="72563-279">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="72563-279">Optional.</span></span> <span data-ttu-id="72563-280">Ten atrybut nie może być używany, jeśli `partition-key` jest używany.</span><span class="sxs-lookup"><span data-stu-id="72563-280">This attribute may not be used if `partition-key` is used.</span></span>|  
|<span data-ttu-id="72563-281">Klucz partycji</span><span class="sxs-lookup"><span data-stu-id="72563-281">partition-key</span></span>|<span data-ttu-id="72563-282">Określa wartość służącą do przypisania partycji podczas wysyłania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="72563-282">Specifies the value used for partition assignment when messages are sent.</span></span>|<span data-ttu-id="72563-283">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="72563-283">Optional.</span></span> <span data-ttu-id="72563-284">Ten atrybut nie może być używany, jeśli `partition-id` jest używany.</span><span class="sxs-lookup"><span data-stu-id="72563-284">This attribute may not be used if `partition-id` is used.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="72563-285">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="72563-285">Usage</span></span>  
 <span data-ttu-id="72563-286">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72563-286">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72563-287">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="72563-287">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="72563-288">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="72563-288">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="72563-289"><a name="mock-response"></a>Zasymulować odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="72563-289"><a name="mock-response"></a> Mock response</span></span>  
<span data-ttu-id="72563-290">`mock-response`, Jak nazwa oznacza, służy do mock operacji i interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="72563-290">The `mock-response`, as the name implies, is used to mock APIs and operations.</span></span> <span data-ttu-id="72563-291">Przerywa wykonywanie normalny potok, a zwraca mocked odpowiedź do obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="72563-291">It aborts normal pipeline execution and returns a mocked response to the caller.</span></span> <span data-ttu-id="72563-292">Zasady zawsze próbuje zwrócić odpowiedzi wierności najwyższy.</span><span class="sxs-lookup"><span data-stu-id="72563-292">The policy always tries to return responses of highest fidelity.</span></span> <span data-ttu-id="72563-293">Preferuje go przykłady zawartości odpowiedzi, gdy dostępne.</span><span class="sxs-lookup"><span data-stu-id="72563-293">It prefers response content examples, whenever available.</span></span> <span data-ttu-id="72563-294">Generuje on przykładowe odpowiedzi ze schematów, gdy znajdują się schematów i przykłady nie.</span><span class="sxs-lookup"><span data-stu-id="72563-294">It generates sample responses from schemas, when schemas are provided and examples are not.</span></span> <span data-ttu-id="72563-295">W przypadku znalezienia przykłady ani schematów odpowiedzi z zawartością, nie są zwracane.</span><span class="sxs-lookup"><span data-stu-id="72563-295">If neither examples or schemas are found, responses with no content are returned.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="72563-296">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="72563-296">Policy statement</span></span>  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="72563-297">Przykłady</span><span class="sxs-lookup"><span data-stu-id="72563-297">Examples</span></span>  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, the content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, the content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a><span data-ttu-id="72563-298">Elementy</span><span class="sxs-lookup"><span data-stu-id="72563-298">Elements</span></span>  
  
|<span data-ttu-id="72563-299">Element</span><span class="sxs-lookup"><span data-stu-id="72563-299">Element</span></span>|<span data-ttu-id="72563-300">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-300">Description</span></span>|<span data-ttu-id="72563-301">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-301">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="72563-302">makiety odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="72563-302">mock-response</span></span>|<span data-ttu-id="72563-303">Element główny.</span><span class="sxs-lookup"><span data-stu-id="72563-303">Root element.</span></span>|<span data-ttu-id="72563-304">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-304">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72563-305">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="72563-305">Attributes</span></span>  
  
|<span data-ttu-id="72563-306">Atrybut</span><span class="sxs-lookup"><span data-stu-id="72563-306">Attribute</span></span>|<span data-ttu-id="72563-307">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-307">Description</span></span>|<span data-ttu-id="72563-308">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-308">Required</span></span>|<span data-ttu-id="72563-309">Domyślne</span><span class="sxs-lookup"><span data-stu-id="72563-309">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="72563-310">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="72563-310">status-code</span></span>|<span data-ttu-id="72563-311">Określa kod stanu odpowiedzi i umożliwia wybranie odpowiedniego przykład lub schematu.</span><span class="sxs-lookup"><span data-stu-id="72563-311">Specifies response status code and is used to select corresponding example or schema.</span></span>|<span data-ttu-id="72563-312">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-312">No</span></span>|<span data-ttu-id="72563-313">200</span><span class="sxs-lookup"><span data-stu-id="72563-313">200</span></span>|  
|<span data-ttu-id="72563-314">Typ zawartości</span><span class="sxs-lookup"><span data-stu-id="72563-314">content-type</span></span>|<span data-ttu-id="72563-315">Określa `Content-Type` wartość nagłówka odpowiedzi i umożliwia wybranie odpowiedniego przykład lub schematu.</span><span class="sxs-lookup"><span data-stu-id="72563-315">Specifies `Content-Type` response header value and is used to select corresponding example or schema.</span></span>|<span data-ttu-id="72563-316">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-316">No</span></span>|<span data-ttu-id="72563-317">Brak</span><span class="sxs-lookup"><span data-stu-id="72563-317">None</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="72563-318">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="72563-318">Usage</span></span>  
 <span data-ttu-id="72563-319">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72563-319">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72563-320">**Sekcje zasad:** przychodzące, wychodzące, na błąd</span><span class="sxs-lookup"><span data-stu-id="72563-320">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="72563-321">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="72563-321">**Policy scopes:** all scopes</span></span>

##  <span data-ttu-id="72563-322"><a name="Retry"></a>Spróbuj ponownie</span><span class="sxs-lookup"><span data-stu-id="72563-322"><a name="Retry"></a> Retry</span></span>  
 <span data-ttu-id="72563-323">`retry` Zasad jego zasad podrzędnych jest wykonywana raz i ponowi próbę ich wykonanie do momentu retry `condition` staje się `false` lub ponów próbę `count` jest wyczerpana.</span><span class="sxs-lookup"><span data-stu-id="72563-323">The             `retry` policy executes its child policies once and then retries their execution until the retry `condition` becomes            `false` or retry            `count` is exhausted.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="72563-324">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="72563-324">Policy statement</span></span>  
  
```xml  
  
<retry  
    condition="boolean expression or literal"  
    count="number of retry attempts"  
    interval="retry interval in seconds"  
    max-interval="maximum retry interval in seconds"  
    delta="retry interval delta in seconds"  
    first-fast-retry="boolean expression or literal">  
        <!-- One or more child policies. No restrictions -->  
</retry>  
  
```  
  
### <a name="example"></a><span data-ttu-id="72563-325">Przykład</span><span class="sxs-lookup"><span data-stu-id="72563-325">Example</span></span>  
 <span data-ttu-id="72563-326">W poniższych przykład forewarding próba zostanie ponowiona maksymalnie 10 razy przy użyciu wykładniczej ponów algorytmu.</span><span class="sxs-lookup"><span data-stu-id="72563-326">In the following example request forewarding is retried up to ten times using exponential retry algorithm.</span></span> <span data-ttu-id="72563-327">Ponieważ `first-fast-retry` jest ustawiona na false, wszystkie ponownych prób podlegają exponsntial Algorytm ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="72563-327">Since                    `first-fast-retry` is set to false, all retry attempts are subject to the exponsntial retry algorithm.</span></span>  
  
```xml  
  
<retry  
    condition="@(context.Response.StatusCode == 500)"  
    count="10"  
    interval="10"  
    max-interval="100"  
    delta="10"  
    first-fast-retry="false">  
        <forward-request />  
</retry>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="72563-328">Elementy</span><span class="sxs-lookup"><span data-stu-id="72563-328">Elements</span></span>  
  
|<span data-ttu-id="72563-329">Element</span><span class="sxs-lookup"><span data-stu-id="72563-329">Element</span></span>|<span data-ttu-id="72563-330">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-330">Description</span></span>|<span data-ttu-id="72563-331">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-331">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="72563-332">Spróbuj ponownie</span><span class="sxs-lookup"><span data-stu-id="72563-332">retry</span></span>|<span data-ttu-id="72563-333">Element główny.</span><span class="sxs-lookup"><span data-stu-id="72563-333">Root element.</span></span> <span data-ttu-id="72563-334">Może zawierać inne zasady jako jego elementy podrzędne.</span><span class="sxs-lookup"><span data-stu-id="72563-334">May contain any other policies as its child elements.</span></span>|<span data-ttu-id="72563-335">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-335">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72563-336">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="72563-336">Attributes</span></span>  
  
|<span data-ttu-id="72563-337">Atrybut</span><span class="sxs-lookup"><span data-stu-id="72563-337">Attribute</span></span>|<span data-ttu-id="72563-338">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-338">Description</span></span>|<span data-ttu-id="72563-339">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-339">Required</span></span>|<span data-ttu-id="72563-340">Domyślne</span><span class="sxs-lookup"><span data-stu-id="72563-340">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="72563-341">Warunek</span><span class="sxs-lookup"><span data-stu-id="72563-341">condition</span></span>|<span data-ttu-id="72563-342">Logiczna literał lub [wyrażenie](api-management-policy-expressions.md) określenie ponownych prób powinna zostać zatrzymana (`false`) lub nadal (`true`).</span><span class="sxs-lookup"><span data-stu-id="72563-342">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span></span>|<span data-ttu-id="72563-343">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-343">Yes</span></span>|<span data-ttu-id="72563-344">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="72563-344">N/A</span></span>|  
|<span data-ttu-id="72563-345">Liczba</span><span class="sxs-lookup"><span data-stu-id="72563-345">count</span></span>|<span data-ttu-id="72563-346">Liczba dodatnia określająca maksymalną liczbę ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="72563-346">A positive number specifying the maximum number of retries to attempt.</span></span>|<span data-ttu-id="72563-347">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-347">Yes</span></span>|<span data-ttu-id="72563-348">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="72563-348">N/A</span></span>|  
|<span data-ttu-id="72563-349">Interwał</span><span class="sxs-lookup"><span data-stu-id="72563-349">interval</span></span>|<span data-ttu-id="72563-350">Liczba dodatnia, w sekundach, określając oczekiwania interwału ponawiania prób.</span><span class="sxs-lookup"><span data-stu-id="72563-350">A positive number in seconds specifying the wait interval between the retry attempts.</span></span>|<span data-ttu-id="72563-351">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-351">Yes</span></span>|<span data-ttu-id="72563-352">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="72563-352">N/A</span></span>|  
|<span data-ttu-id="72563-353">Maksymalny interwał</span><span class="sxs-lookup"><span data-stu-id="72563-353">max-interval</span></span>|<span data-ttu-id="72563-354">Liczba dodatnia, w sekundach określający maksymalną poczekaj interwał między ponownymi próbami.</span><span class="sxs-lookup"><span data-stu-id="72563-354">A positive number in seconds specifying the maximum wait interval between the retry attempts.</span></span> <span data-ttu-id="72563-355">Służy do implementowania algorytm wykładnicze ponów próbę.</span><span class="sxs-lookup"><span data-stu-id="72563-355">It is used to implement an exponential retry algorithm.</span></span>|<span data-ttu-id="72563-356">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-356">No</span></span>|<span data-ttu-id="72563-357">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="72563-357">N/A</span></span>|  
|<span data-ttu-id="72563-358">delta</span><span class="sxs-lookup"><span data-stu-id="72563-358">delta</span></span>|<span data-ttu-id="72563-359">Liczba dodatnia, w sekundach, określając przyrost interwału oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="72563-359">A positive number in seconds specifying the wait interval increment.</span></span> <span data-ttu-id="72563-360">Służy do zaimplementowania algorytmów liniowej i wykładniczej ponów próbę.</span><span class="sxs-lookup"><span data-stu-id="72563-360">It is used to implement the linear and exponential retry algorithms.</span></span>|<span data-ttu-id="72563-361">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-361">No</span></span>|<span data-ttu-id="72563-362">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="72563-362">N/A</span></span>|  
|<span data-ttu-id="72563-363">pierwszy ponownej próby fast</span><span class="sxs-lookup"><span data-stu-id="72563-363">first-fast-retry</span></span>|<span data-ttu-id="72563-364">Jeśli ustawiono `true` , pierwszy ponowienia próby jest wykonywane bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="72563-364">If set to                                    `true` , the first retry attempt is performed immediately.</span></span>|<span data-ttu-id="72563-365">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-365">No</span></span>|`false`|  
  
> [!NOTE]
>  <span data-ttu-id="72563-366">Gdy tylko `interval` jest określony, **stałej** są wykonywane Interwał ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="72563-366">When only the `interval` is specified, **fixed** interval retries are performed.</span></span>  
>  <span data-ttu-id="72563-367">Gdy tylko `interval` i `delta` są określone, **liniowej** interwału ponawiania algorytm jest używany, gdy czas oczekiwania między kolejnymi próbami jest obliczana według następującego wzoru - `interval + (count - 1)*delta`.</span><span class="sxs-lookup"><span data-stu-id="72563-367">When only the `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according the following formula - `interval + (count - 1)*delta`.</span></span>  
>  <span data-ttu-id="72563-368">Gdy `interval`, `max-interval` i `delta` są określone, **wykładniczej** interwału ponawiania algorytm jest stosowana, gdy czas oczekiwania między kolejnymi próbami rośnie wykładniczo od wartości `interval` wartość `max-interval` zgodnie z następujących forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span><span class="sxs-lookup"><span data-stu-id="72563-368">When the `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where the wait time between the retries is growing exponentially from the value of `interval` to the value `max-interval` according to the following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span></span>  
  
### <a name="usage"></a><span data-ttu-id="72563-369">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="72563-369">Usage</span></span>  
 <span data-ttu-id="72563-370">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="72563-370">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span> <span data-ttu-id="72563-371">Należy pamiętać, że ograniczenia użycia zasad podrzędne będą dziedziczone przez te zasady.</span><span class="sxs-lookup"><span data-stu-id="72563-371">Note that child policy usage restrictions will be inherited by this policy.</span></span>  
  
-   <span data-ttu-id="72563-372">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="72563-372">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="72563-373">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="72563-373">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="72563-374"><a name="ReturnResponse"></a>Odpowiedź zwrócona</span><span class="sxs-lookup"><span data-stu-id="72563-374"><a name="ReturnResponse"></a> Return response</span></span>  
 <span data-ttu-id="72563-375">`return-response` Zasad przerwanie wykonywania potoku i zwraca domyślnego lub niestandardowego odpowiedź do obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="72563-375">The `return-response` policy aborts pipeline execution and returns either a default or custom response to the caller.</span></span> <span data-ttu-id="72563-376">Domyślny jest `200 OK` nie jednostki.</span><span class="sxs-lookup"><span data-stu-id="72563-376">Default response is `200 OK` with no body.</span></span> <span data-ttu-id="72563-377">Za pomocą instrukcji kontekstu zmiennej lub zasad można określić niestandardową odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="72563-377">Custom response can be specified via a context variable or policy statements.</span></span> <span data-ttu-id="72563-378">Zarówno udostępniane odpowiedzi zawarty w zmiennej kontekstu, która jest modyfikowany przez deklaracji zasad przed zwróceniem do obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="72563-378">When both are provided, the response contained within the context variable is modified by the policy statements before being returned to the caller.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="72563-379">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="72563-379">Policy statement</span></span>  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a><span data-ttu-id="72563-380">Przykład</span><span class="sxs-lookup"><span data-stu-id="72563-380">Example</span></span>  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="72563-381">Elementy</span><span class="sxs-lookup"><span data-stu-id="72563-381">Elements</span></span>  
  
|<span data-ttu-id="72563-382">Element</span><span class="sxs-lookup"><span data-stu-id="72563-382">Element</span></span>|<span data-ttu-id="72563-383">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-383">Description</span></span>|<span data-ttu-id="72563-384">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-384">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="72563-385">odpowiedź Return</span><span class="sxs-lookup"><span data-stu-id="72563-385">return-response</span></span>|<span data-ttu-id="72563-386">Element główny.</span><span class="sxs-lookup"><span data-stu-id="72563-386">Root element.</span></span>|<span data-ttu-id="72563-387">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-387">Yes</span></span>|  
|<span data-ttu-id="72563-388">set — nagłówek</span><span class="sxs-lookup"><span data-stu-id="72563-388">set-header</span></span>|<span data-ttu-id="72563-389">A [nagłówka set](api-management-transformation-policies.md#SetHTTPheader) deklaracji zasad.</span><span class="sxs-lookup"><span data-stu-id="72563-389">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span></span>|<span data-ttu-id="72563-390">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-390">No</span></span>|  
|<span data-ttu-id="72563-391">zestaw treści</span><span class="sxs-lookup"><span data-stu-id="72563-391">set-body</span></span>|<span data-ttu-id="72563-392">A [treści zestaw](api-management-transformation-policies.md#SetBody) deklaracji zasad.</span><span class="sxs-lookup"><span data-stu-id="72563-392">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span></span>|<span data-ttu-id="72563-393">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-393">No</span></span>|  
|<span data-ttu-id="72563-394">Ustaw stan</span><span class="sxs-lookup"><span data-stu-id="72563-394">set-status</span></span>|<span data-ttu-id="72563-395">A [Ustaw stan](api-management-advanced-policies.md#SetStatus) deklaracji zasad.</span><span class="sxs-lookup"><span data-stu-id="72563-395">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span></span>|<span data-ttu-id="72563-396">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-396">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72563-397">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="72563-397">Attributes</span></span>  
  
|<span data-ttu-id="72563-398">Atrybut</span><span class="sxs-lookup"><span data-stu-id="72563-398">Attribute</span></span>|<span data-ttu-id="72563-399">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-399">Description</span></span>|<span data-ttu-id="72563-400">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-400">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="72563-401">Nazwa zmiennej odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="72563-401">response-variable-name</span></span>|<span data-ttu-id="72563-402">Nazwa zmiennej kontekstu, która odwołuje się do z, na przykład nadrzędnym [żądanie wysłania](api-management-advanced-policies.md#SendRequest) zasad i zawierający `Response` obiektu</span><span class="sxs-lookup"><span data-stu-id="72563-402">The name of the context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span></span>|<span data-ttu-id="72563-403">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="72563-403">Optional.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="72563-404">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="72563-404">Usage</span></span>  
 <span data-ttu-id="72563-405">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72563-405">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72563-406">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="72563-406">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="72563-407">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="72563-407">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="72563-408"><a name="SendOneWayRequest"></a>Wyślij żądanie jednokierunkowej</span><span class="sxs-lookup"><span data-stu-id="72563-408"><a name="SendOneWayRequest"></a> Send one way request</span></span>  
 <span data-ttu-id="72563-409">`send-one-way-request` Zasad wysyła żądanie podana pod określony adres URL bez oczekiwania na odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="72563-409">The `send-one-way-request` policy sends the provided request to the specified URL without waiting for a response.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="72563-410">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="72563-410">Policy statement</span></span>  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="72563-411">Przykład</span><span class="sxs-lookup"><span data-stu-id="72563-411">Example</span></span>  
 <span data-ttu-id="72563-412">Ta zasada przykładowych pokazano przykład przy użyciu `send-one-way-request` zasad, aby wysłać wiadomość Slack pokoju rozmów, jeśli kod odpowiedzi HTTP jest większa niż lub równa 500.</span><span class="sxs-lookup"><span data-stu-id="72563-412">This sample policy shows an example of using the `send-one-way-request` policy to send a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span></span> <span data-ttu-id="72563-413">Aby uzyskać więcej informacji na ten przykład, zobacz [za pomocą usług zewnętrznych z usługi Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="72563-413">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="72563-414">Elementy</span><span class="sxs-lookup"><span data-stu-id="72563-414">Elements</span></span>  
  
|<span data-ttu-id="72563-415">Element</span><span class="sxs-lookup"><span data-stu-id="72563-415">Element</span></span>|<span data-ttu-id="72563-416">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-416">Description</span></span>|<span data-ttu-id="72563-417">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-417">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="72563-418">sposób żądania, Wyślij co w-</span><span class="sxs-lookup"><span data-stu-id="72563-418">send-one-way-request</span></span>|<span data-ttu-id="72563-419">Element główny.</span><span class="sxs-lookup"><span data-stu-id="72563-419">Root element.</span></span>|<span data-ttu-id="72563-420">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-420">Yes</span></span>|  
|<span data-ttu-id="72563-421">adres URL</span><span class="sxs-lookup"><span data-stu-id="72563-421">url</span></span>|<span data-ttu-id="72563-422">Adres URL żądania.</span><span class="sxs-lookup"><span data-stu-id="72563-422">The URL of the request.</span></span>|<span data-ttu-id="72563-423">Jeśli nie trybu = kopiowania; tak, w przeciwnym razie wartość.</span><span class="sxs-lookup"><span data-stu-id="72563-423">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="72563-424">— Metoda</span><span class="sxs-lookup"><span data-stu-id="72563-424">method</span></span>|<span data-ttu-id="72563-425">Metoda HTTP dla żądania.</span><span class="sxs-lookup"><span data-stu-id="72563-425">The HTTP method for the request.</span></span>|<span data-ttu-id="72563-426">Jeśli nie trybu = kopiowania; tak, w przeciwnym razie wartość.</span><span class="sxs-lookup"><span data-stu-id="72563-426">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="72563-427">nagłówek</span><span class="sxs-lookup"><span data-stu-id="72563-427">header</span></span>|<span data-ttu-id="72563-428">Nagłówek żądania.</span><span class="sxs-lookup"><span data-stu-id="72563-428">Request header.</span></span> <span data-ttu-id="72563-429">Użyj wielu elementów nagłówka dla wielu nagłówków żądania.</span><span class="sxs-lookup"><span data-stu-id="72563-429">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="72563-430">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-430">No</span></span>|  
|<span data-ttu-id="72563-431">Treści</span><span class="sxs-lookup"><span data-stu-id="72563-431">body</span></span>|<span data-ttu-id="72563-432">Treść żądania.</span><span class="sxs-lookup"><span data-stu-id="72563-432">The request body.</span></span>|<span data-ttu-id="72563-433">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-433">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72563-434">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="72563-434">Attributes</span></span>  
  
|<span data-ttu-id="72563-435">Atrybut</span><span class="sxs-lookup"><span data-stu-id="72563-435">Attribute</span></span>|<span data-ttu-id="72563-436">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-436">Description</span></span>|<span data-ttu-id="72563-437">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-437">Required</span></span>|<span data-ttu-id="72563-438">Domyślne</span><span class="sxs-lookup"><span data-stu-id="72563-438">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="72563-439">tryb = "string"</span><span class="sxs-lookup"><span data-stu-id="72563-439">mode="string"</span></span>|<span data-ttu-id="72563-440">Określa, czy jest to nowe żądanie lub kopię bieżącego żądania.</span><span class="sxs-lookup"><span data-stu-id="72563-440">Determines whether this is a new request or a copy of the current request.</span></span> <span data-ttu-id="72563-441">W trybie wychodzących tryb = kopiowania nie inicjuje treści żądania.</span><span class="sxs-lookup"><span data-stu-id="72563-441">In outbound mode, mode=copy does not initialize the request body.</span></span>|<span data-ttu-id="72563-442">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-442">No</span></span>|<span data-ttu-id="72563-443">Nowy</span><span class="sxs-lookup"><span data-stu-id="72563-443">New</span></span>|  
|<span data-ttu-id="72563-444">name</span><span class="sxs-lookup"><span data-stu-id="72563-444">name</span></span>|<span data-ttu-id="72563-445">Określa nazwę nagłówka do ustawienia.</span><span class="sxs-lookup"><span data-stu-id="72563-445">Specifies the name of the header to be set.</span></span>|<span data-ttu-id="72563-446">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-446">Yes</span></span>|<span data-ttu-id="72563-447">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="72563-447">N/A</span></span>|  
|<span data-ttu-id="72563-448">istnieje akcja</span><span class="sxs-lookup"><span data-stu-id="72563-448">exists-action</span></span>|<span data-ttu-id="72563-449">Określa, jakie działania w sytuacji, gdy nagłówek został już określony.</span><span class="sxs-lookup"><span data-stu-id="72563-449">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="72563-450">Ten atrybut musi mieć jedną z następujących wartości.</span><span class="sxs-lookup"><span data-stu-id="72563-450">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="72563-451">-override - zastępuje wartość istniejący nagłówek.</span><span class="sxs-lookup"><span data-stu-id="72563-451">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="72563-452">-skip — nie zastępuje istniejącą wartość nagłówka.</span><span class="sxs-lookup"><span data-stu-id="72563-452">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="72563-453">-dołączania - dołącza wartość do istniejącej wartości nagłówka.</span><span class="sxs-lookup"><span data-stu-id="72563-453">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="72563-454">-Usunięcie — usuwa nagłówek z żądania.</span><span class="sxs-lookup"><span data-stu-id="72563-454">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="72563-455">Jeśli wartość `override` powoduje rejestrowanie wiele wpisów o takiej samej nazwie w nagłówku ustawiany zgodnie ze wszystkich zapisów (które zostaną wyświetlone wiele razy); zostanie ustawiona tylko wartości wyświetlane w wynikach.</span><span class="sxs-lookup"><span data-stu-id="72563-455">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="72563-456">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-456">No</span></span>|<span data-ttu-id="72563-457">zastąpienie</span><span class="sxs-lookup"><span data-stu-id="72563-457">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="72563-458">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="72563-458">Usage</span></span>  
 <span data-ttu-id="72563-459">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72563-459">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72563-460">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="72563-460">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="72563-461">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="72563-461">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="72563-462"><a name="SendRequest"></a>Wyślij żądanie</span><span class="sxs-lookup"><span data-stu-id="72563-462"><a name="SendRequest"></a> Send request</span></span>  
 <span data-ttu-id="72563-463">`send-request` Zasad wysyła żądanie podana pod określony adres URL już ustaw wartość limitu czasu oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="72563-463">The `send-request` policy sends the provided request to the specified URL, waiting no longer than the set timeout value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="72563-464">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="72563-464">Policy statement</span></span>  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="72563-465">Przykład</span><span class="sxs-lookup"><span data-stu-id="72563-465">Example</span></span>  
 <span data-ttu-id="72563-466">Ten przykład przedstawia jedną z metod można zweryfikować odwołania do tokenu z serwera autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="72563-466">This example shows one way to verify a reference token with an authorization server.</span></span> <span data-ttu-id="72563-467">Aby uzyskać więcej informacji na ten przykład, zobacz [za pomocą usług zewnętrznych z usługi Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="72563-467">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request to Token Server to validate token (see RFC 7662) -->  
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">  
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>  
    <set-method>POST</set-method>  
    <set-header name="Authorization" exists-action="override">  
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>  
    </set-header>  
    <set-header name="Content-Type" exists-action="override">  
      <value>application/x-www-form-urlencoded</value>  
    </set-header>  
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>  
  </send-request>  
  
  <choose>  
        <!-- Check active property in response -->  
        <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
            <!-- Return 401 Unauthorized with http-problem payload -->  
            <return-response response-variable-name="existing response variable">  
                <set-status code="401" reason="Unauthorized" />  
                <set-header name="WWW-Authenticate" exists-action="override">  
                    <value>Bearer error="invalid_token"</value>  
                </set-header>  
            </return-response>  
        </when>  
    </choose>  
  <base />  
</inbound>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="72563-468">Elementy</span><span class="sxs-lookup"><span data-stu-id="72563-468">Elements</span></span>  
  
|<span data-ttu-id="72563-469">Element</span><span class="sxs-lookup"><span data-stu-id="72563-469">Element</span></span>|<span data-ttu-id="72563-470">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-470">Description</span></span>|<span data-ttu-id="72563-471">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-471">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="72563-472">Żądanie wysłania</span><span class="sxs-lookup"><span data-stu-id="72563-472">send-request</span></span>|<span data-ttu-id="72563-473">Element główny.</span><span class="sxs-lookup"><span data-stu-id="72563-473">Root element.</span></span>|<span data-ttu-id="72563-474">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-474">Yes</span></span>|  
|<span data-ttu-id="72563-475">adres URL</span><span class="sxs-lookup"><span data-stu-id="72563-475">url</span></span>|<span data-ttu-id="72563-476">Adres URL żądania.</span><span class="sxs-lookup"><span data-stu-id="72563-476">The URL of the request.</span></span>|<span data-ttu-id="72563-477">Jeśli nie trybu = kopiowania; tak, w przeciwnym razie wartość.</span><span class="sxs-lookup"><span data-stu-id="72563-477">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="72563-478">— Metoda</span><span class="sxs-lookup"><span data-stu-id="72563-478">method</span></span>|<span data-ttu-id="72563-479">Metoda HTTP dla żądania.</span><span class="sxs-lookup"><span data-stu-id="72563-479">The HTTP method for the request.</span></span>|<span data-ttu-id="72563-480">Jeśli nie trybu = kopiowania; tak, w przeciwnym razie wartość.</span><span class="sxs-lookup"><span data-stu-id="72563-480">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="72563-481">nagłówek</span><span class="sxs-lookup"><span data-stu-id="72563-481">header</span></span>|<span data-ttu-id="72563-482">Nagłówek żądania.</span><span class="sxs-lookup"><span data-stu-id="72563-482">Request header.</span></span> <span data-ttu-id="72563-483">Użyj wielu elementów nagłówka dla wielu nagłówków żądania.</span><span class="sxs-lookup"><span data-stu-id="72563-483">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="72563-484">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-484">No</span></span>|  
|<span data-ttu-id="72563-485">Treści</span><span class="sxs-lookup"><span data-stu-id="72563-485">body</span></span>|<span data-ttu-id="72563-486">Treść żądania.</span><span class="sxs-lookup"><span data-stu-id="72563-486">The request body.</span></span>|<span data-ttu-id="72563-487">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-487">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72563-488">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="72563-488">Attributes</span></span>  
  
|<span data-ttu-id="72563-489">Atrybut</span><span class="sxs-lookup"><span data-stu-id="72563-489">Attribute</span></span>|<span data-ttu-id="72563-490">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-490">Description</span></span>|<span data-ttu-id="72563-491">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-491">Required</span></span>|<span data-ttu-id="72563-492">Domyślne</span><span class="sxs-lookup"><span data-stu-id="72563-492">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="72563-493">tryb = "string"</span><span class="sxs-lookup"><span data-stu-id="72563-493">mode="string"</span></span>|<span data-ttu-id="72563-494">Określa, czy jest to nowe żądanie lub kopię bieżącego żądania.</span><span class="sxs-lookup"><span data-stu-id="72563-494">Determines whether this is a new request or a copy of the current request.</span></span> <span data-ttu-id="72563-495">W trybie wychodzących tryb = kopiowania nie inicjuje treści żądania.</span><span class="sxs-lookup"><span data-stu-id="72563-495">In outbound mode, mode=copy does not initialize the request body.</span></span>|<span data-ttu-id="72563-496">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-496">No</span></span>|<span data-ttu-id="72563-497">Nowy</span><span class="sxs-lookup"><span data-stu-id="72563-497">New</span></span>|  
|<span data-ttu-id="72563-498">Nazwa zmiennej odpowiedzi = "string"</span><span class="sxs-lookup"><span data-stu-id="72563-498">response-variable-name="string"</span></span>|<span data-ttu-id="72563-499">Jeśli nie istnieje `context.Response` jest używany.</span><span class="sxs-lookup"><span data-stu-id="72563-499">If not present, `context.Response` is used.</span></span>|<span data-ttu-id="72563-500">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-500">No</span></span>|<span data-ttu-id="72563-501">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="72563-501">N/A</span></span>|  
|<span data-ttu-id="72563-502">limit czasu = "int"</span><span class="sxs-lookup"><span data-stu-id="72563-502">timeout="integer"</span></span>|<span data-ttu-id="72563-503">Interwał limitu czasu w sekundach przed wywołaniem do adresu URL nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="72563-503">The timeout interval in seconds before the call to the URL fails.</span></span>|<span data-ttu-id="72563-504">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-504">No</span></span>|<span data-ttu-id="72563-505">60</span><span class="sxs-lookup"><span data-stu-id="72563-505">60</span></span>|  
|<span data-ttu-id="72563-506">Ignoruj błąd</span><span class="sxs-lookup"><span data-stu-id="72563-506">ignore-error</span></span>|<span data-ttu-id="72563-507">Jeśli wartość PRAWDA, a wyniki żądania w błąd:</span><span class="sxs-lookup"><span data-stu-id="72563-507">If true and the request results in an error:</span></span><br /><br /> <span data-ttu-id="72563-508">— Jeśli nazwa zmiennej odpowiedzi został określony, będzie zawierać wartości null.</span><span class="sxs-lookup"><span data-stu-id="72563-508">-   If response-variable-name was specified it will contain a null value.</span></span><br /><span data-ttu-id="72563-509">— Jeśli nie określono odpowiedzi zmienna nazwy, kontekstu. Żądanie nie zostanie zaktualizowany.</span><span class="sxs-lookup"><span data-stu-id="72563-509">-   If response-variable-name was not specified, context.Request will not be updated.</span></span>|<span data-ttu-id="72563-510">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-510">No</span></span>|<span data-ttu-id="72563-511">wartość false</span><span class="sxs-lookup"><span data-stu-id="72563-511">false</span></span>|  
|<span data-ttu-id="72563-512">name</span><span class="sxs-lookup"><span data-stu-id="72563-512">name</span></span>|<span data-ttu-id="72563-513">Określa nazwę nagłówka do ustawienia.</span><span class="sxs-lookup"><span data-stu-id="72563-513">Specifies the name of the header to be set.</span></span>|<span data-ttu-id="72563-514">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-514">Yes</span></span>|<span data-ttu-id="72563-515">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="72563-515">N/A</span></span>|  
|<span data-ttu-id="72563-516">istnieje akcja</span><span class="sxs-lookup"><span data-stu-id="72563-516">exists-action</span></span>|<span data-ttu-id="72563-517">Określa, jakie działania w sytuacji, gdy nagłówek został już określony.</span><span class="sxs-lookup"><span data-stu-id="72563-517">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="72563-518">Ten atrybut musi mieć jedną z następujących wartości.</span><span class="sxs-lookup"><span data-stu-id="72563-518">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="72563-519">-override - zastępuje wartość istniejący nagłówek.</span><span class="sxs-lookup"><span data-stu-id="72563-519">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="72563-520">-skip — nie zastępuje istniejącą wartość nagłówka.</span><span class="sxs-lookup"><span data-stu-id="72563-520">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="72563-521">-dołączania - dołącza wartość do istniejącej wartości nagłówka.</span><span class="sxs-lookup"><span data-stu-id="72563-521">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="72563-522">-Usunięcie — usuwa nagłówek z żądania.</span><span class="sxs-lookup"><span data-stu-id="72563-522">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="72563-523">Jeśli wartość `override` powoduje rejestrowanie wiele wpisów o takiej samej nazwie w nagłówku ustawiany zgodnie ze wszystkich zapisów (które zostaną wyświetlone wiele razy); zostanie ustawiona tylko wartości wyświetlane w wynikach.</span><span class="sxs-lookup"><span data-stu-id="72563-523">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="72563-524">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-524">No</span></span>|<span data-ttu-id="72563-525">zastąpienie</span><span class="sxs-lookup"><span data-stu-id="72563-525">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="72563-526">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="72563-526">Usage</span></span>  
 <span data-ttu-id="72563-527">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72563-527">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72563-528">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="72563-528">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="72563-529">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="72563-529">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="72563-530"><a name="SetHttpProxy"></a>Serwer proxy HTTP zestawu</span><span class="sxs-lookup"><span data-stu-id="72563-530"><a name="SetHttpProxy"></a> Set HTTP proxy</span></span>  
 <span data-ttu-id="72563-531">`proxy` Zasad umożliwia rozsyłanie żądań przekazywane do zapleczy za pośrednictwem serwera proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="72563-531">The `proxy` policy allows you to route requests forwarded to backends via an HTTP proxy.</span></span> <span data-ttu-id="72563-532">HTTP (a nie HTTPS) jest obsługiwana między bramy i serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="72563-532">Only HTTP (not HTTPS) is supported between the gateway and the proxy.</span></span> <span data-ttu-id="72563-533">Podstawowe i tylko z uwierzytelniania NTLM.</span><span class="sxs-lookup"><span data-stu-id="72563-533">Basic and NTLM authentication only.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="72563-534">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="72563-534">Policy statement</span></span>  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="72563-535">Przykład</span><span class="sxs-lookup"><span data-stu-id="72563-535">Example</span></span>  
<span data-ttu-id="72563-536">Zwróć uwagę na użycie [właściwości](api-management-howto-properties.md) jako wartości nazwy użytkownika i hasło, aby uniknąć poufne informacje są przechowywane w dokumencie zasady.</span><span class="sxs-lookup"><span data-stu-id="72563-536">Note the use of [properties](api-management-howto-properties.md) as values of the username and password to avoid storing sensitive information in the policy document.</span></span>  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a><span data-ttu-id="72563-537">Elementy</span><span class="sxs-lookup"><span data-stu-id="72563-537">Elements</span></span>  
  
|<span data-ttu-id="72563-538">Element</span><span class="sxs-lookup"><span data-stu-id="72563-538">Element</span></span>|<span data-ttu-id="72563-539">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-539">Description</span></span>|<span data-ttu-id="72563-540">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-540">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="72563-541">Serwer proxy</span><span class="sxs-lookup"><span data-stu-id="72563-541">proxy</span></span>|<span data-ttu-id="72563-542">Element główny</span><span class="sxs-lookup"><span data-stu-id="72563-542">Root element</span></span>|<span data-ttu-id="72563-543">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-543">Yes</span></span>|  

### <a name="attributes"></a><span data-ttu-id="72563-544">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="72563-544">Attributes</span></span>  
  
|<span data-ttu-id="72563-545">Atrybut</span><span class="sxs-lookup"><span data-stu-id="72563-545">Attribute</span></span>|<span data-ttu-id="72563-546">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-546">Description</span></span>|<span data-ttu-id="72563-547">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-547">Required</span></span>|<span data-ttu-id="72563-548">Domyślne</span><span class="sxs-lookup"><span data-stu-id="72563-548">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="72563-549">adres URL = "string"</span><span class="sxs-lookup"><span data-stu-id="72563-549">url="string"</span></span>|<span data-ttu-id="72563-550">Adres URL serwera proxy w postaci http://host:port.</span><span class="sxs-lookup"><span data-stu-id="72563-550">Proxy URL in the form of http://host:port.</span></span>|<span data-ttu-id="72563-551">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-551">Yes</span></span>|<span data-ttu-id="72563-552">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="72563-552">N/A</span></span>|  
|<span data-ttu-id="72563-553">Nazwa użytkownika = "string"</span><span class="sxs-lookup"><span data-stu-id="72563-553">username="string"</span></span>|<span data-ttu-id="72563-554">Nazwa użytkownika używanego do uwierzytelniania z serwerem proxy.</span><span class="sxs-lookup"><span data-stu-id="72563-554">Username to be used for authentication with the proxy.</span></span>|<span data-ttu-id="72563-555">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-555">No</span></span>|<span data-ttu-id="72563-556">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="72563-556">N/A</span></span>|  
|<span data-ttu-id="72563-557">hasło = "string"</span><span class="sxs-lookup"><span data-stu-id="72563-557">password="string"</span></span>|<span data-ttu-id="72563-558">Hasło będzie używany do uwierzytelniania z serwerem proxy.</span><span class="sxs-lookup"><span data-stu-id="72563-558">Password to be used for authentication with the proxy.</span></span>|<span data-ttu-id="72563-559">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-559">No</span></span>|<span data-ttu-id="72563-560">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="72563-560">N/A</span></span>|  

### <a name="usage"></a><span data-ttu-id="72563-561">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="72563-561">Usage</span></span>  
 <span data-ttu-id="72563-562">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72563-562">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72563-563">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="72563-563">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="72563-564">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="72563-564">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="72563-565"><a name="SetRequestMethod"></a>Set, Metoda żądania</span><span class="sxs-lookup"><span data-stu-id="72563-565"><a name="SetRequestMethod"></a> Set request method</span></span>  
 <span data-ttu-id="72563-566">`set-method` Zasad umożliwia zmianę metody żądania HTTP dla żądania.</span><span class="sxs-lookup"><span data-stu-id="72563-566">The `set-method` policy allows you to change the HTTP request method for a request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="72563-567">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="72563-567">Policy statement</span></span>  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a><span data-ttu-id="72563-568">Przykład</span><span class="sxs-lookup"><span data-stu-id="72563-568">Example</span></span>  
 <span data-ttu-id="72563-569">Przykładowe zasady używa `set-method` zasad przedstawiono przykład wysyłanie wiadomości do Slack pokoju rozmów, jeśli kod odpowiedzi HTTP jest większa niż lub równa 500.</span><span class="sxs-lookup"><span data-stu-id="72563-569">This sample policy that uses the `set-method` policy shows an example of sending a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span></span> <span data-ttu-id="72563-570">Aby uzyskać więcej informacji na ten przykład, zobacz [za pomocą usług zewnętrznych z usługi Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="72563-570">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="72563-571">Elementy</span><span class="sxs-lookup"><span data-stu-id="72563-571">Elements</span></span>  
  
|<span data-ttu-id="72563-572">Element</span><span class="sxs-lookup"><span data-stu-id="72563-572">Element</span></span>|<span data-ttu-id="72563-573">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-573">Description</span></span>|<span data-ttu-id="72563-574">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-574">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="72563-575">set, metoda</span><span class="sxs-lookup"><span data-stu-id="72563-575">set-method</span></span>|<span data-ttu-id="72563-576">Element główny.</span><span class="sxs-lookup"><span data-stu-id="72563-576">Root element.</span></span> <span data-ttu-id="72563-577">Wartość elementu określa metodę HTTP.</span><span class="sxs-lookup"><span data-stu-id="72563-577">The value of the element specifies the HTTP method.</span></span>|<span data-ttu-id="72563-578">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-578">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="72563-579">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="72563-579">Usage</span></span>  
 <span data-ttu-id="72563-580">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72563-580">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72563-581">**Sekcje zasad:** dla ruchu przychodzącego, na błąd</span><span class="sxs-lookup"><span data-stu-id="72563-581">**Policy sections:** inbound, on-error</span></span>  
  
-   <span data-ttu-id="72563-582">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="72563-582">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="72563-583"><a name="SetStatus"></a>Kod stanu zestawu</span><span class="sxs-lookup"><span data-stu-id="72563-583"><a name="SetStatus"></a> Set status code</span></span>  
 <span data-ttu-id="72563-584">`set-status` Zasad ustawia kod stanu HTTP do określonej wartości.</span><span class="sxs-lookup"><span data-stu-id="72563-584">The `set-status` policy sets the HTTP status code to the specified value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="72563-585">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="72563-585">Policy statement</span></span>  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a><span data-ttu-id="72563-586">Przykład</span><span class="sxs-lookup"><span data-stu-id="72563-586">Example</span></span>  
 <span data-ttu-id="72563-587">Ten przykład przedstawia sposób zwracania odpowiedzi 401, jeśli token autoryzacji jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="72563-587">This example shows how to return a 401 response if the authorization token is invalid.</span></span> <span data-ttu-id="72563-588">Aby uzyskać więcej informacji, zobacz [za pomocą usług zewnętrznych z usługi Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span><span class="sxs-lookup"><span data-stu-id="72563-588">For more information, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span></span>  
  
```xml  
<choose>  
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
    <return-response response-variable-name="existing response variable">  
      <set-status code="401" reason="Unauthorized" />  
      <set-header name="WWW-Authenticate" exists-action="override">  
        <value>Bearer error="invalid_token"</value>  
      </set-header>  
    </return-response>  
  </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="72563-589">Elementy</span><span class="sxs-lookup"><span data-stu-id="72563-589">Elements</span></span>  
  
|<span data-ttu-id="72563-590">Element</span><span class="sxs-lookup"><span data-stu-id="72563-590">Element</span></span>|<span data-ttu-id="72563-591">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-591">Description</span></span>|<span data-ttu-id="72563-592">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-592">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="72563-593">Ustaw stan</span><span class="sxs-lookup"><span data-stu-id="72563-593">set-status</span></span>|<span data-ttu-id="72563-594">Element główny.</span><span class="sxs-lookup"><span data-stu-id="72563-594">Root element.</span></span>|<span data-ttu-id="72563-595">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-595">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72563-596">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="72563-596">Attributes</span></span>  
  
|<span data-ttu-id="72563-597">Atrybut</span><span class="sxs-lookup"><span data-stu-id="72563-597">Attribute</span></span>|<span data-ttu-id="72563-598">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-598">Description</span></span>|<span data-ttu-id="72563-599">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-599">Required</span></span>|<span data-ttu-id="72563-600">Domyślne</span><span class="sxs-lookup"><span data-stu-id="72563-600">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="72563-601">Kod = "int"</span><span class="sxs-lookup"><span data-stu-id="72563-601">code="integer"</span></span>|<span data-ttu-id="72563-602">Kod stanu HTTP do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="72563-602">The HTTP status code to return.</span></span>|<span data-ttu-id="72563-603">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-603">Yes</span></span>|<span data-ttu-id="72563-604">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="72563-604">N/A</span></span>|  
|<span data-ttu-id="72563-605">Przyczyna = "string"</span><span class="sxs-lookup"><span data-stu-id="72563-605">reason="string"</span></span>|<span data-ttu-id="72563-606">Opis powodu zwróciło kod stanu.</span><span class="sxs-lookup"><span data-stu-id="72563-606">A description of the reason for returning the status code.</span></span>|<span data-ttu-id="72563-607">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-607">Yes</span></span>|<span data-ttu-id="72563-608">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="72563-608">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="72563-609">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="72563-609">Usage</span></span>  
 <span data-ttu-id="72563-610">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72563-610">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72563-611">**Sekcje zasad:** wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="72563-611">**Policy sections:** outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="72563-612">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="72563-612">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="72563-613"><a name="set-variable"></a>Ustaw zmienną</span><span class="sxs-lookup"><span data-stu-id="72563-613"><a name="set-variable"></a> Set variable</span></span>  
 <span data-ttu-id="72563-614">`set-variable` Deklaruje zasad [kontekstu](api-management-policy-expressions.md#ContextVariables) zmiennej i przypisuje go za pośrednictwem określoną wartość [wyrażenie](api-management-policy-expressions.md) lub literałem ciągu.</span><span class="sxs-lookup"><span data-stu-id="72563-614">The `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span></span> <span data-ttu-id="72563-615">Jeśli wyrażenie zawiera właściwość literal zostanie przekonwertowany na ciąg i typ wartości będzie `System.String`.</span><span class="sxs-lookup"><span data-stu-id="72563-615">if the expression contains a literal it will be converted to a string and the type of the value will be `System.String`.</span></span>  
  
###  <span data-ttu-id="72563-616"><a name="set-variablePolicyStatement"></a>Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="72563-616"><a name="set-variablePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <span data-ttu-id="72563-617"><a name="set-variableExample"></a>Przykład</span><span class="sxs-lookup"><span data-stu-id="72563-617"><a name="set-variableExample"></a> Example</span></span>  
 <span data-ttu-id="72563-618">W poniższym przykładzie pokazano Ustaw zasady zmiennej w sekcji dla ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="72563-618">The following example demonstrates a set variable policy in the inbound section.</span></span> <span data-ttu-id="72563-619">Ta zasada zmiennej zestaw tworzy `isMobile` logiczna [kontekstu](api-management-policy-expressions.md#ContextVariables) zmiennej, która ma ustawioną wartość true, jeśli `User-Agent` tekst zawiera nagłówek żądania `iPad` lub `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="72563-619">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span></span>  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a><span data-ttu-id="72563-620">Elementy</span><span class="sxs-lookup"><span data-stu-id="72563-620">Elements</span></span>  
  
|<span data-ttu-id="72563-621">Element</span><span class="sxs-lookup"><span data-stu-id="72563-621">Element</span></span>|<span data-ttu-id="72563-622">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-622">Description</span></span>|<span data-ttu-id="72563-623">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-623">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="72563-624">Ustaw zmienną</span><span class="sxs-lookup"><span data-stu-id="72563-624">set-variable</span></span>|<span data-ttu-id="72563-625">Element główny.</span><span class="sxs-lookup"><span data-stu-id="72563-625">Root element.</span></span>|<span data-ttu-id="72563-626">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-626">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72563-627">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="72563-627">Attributes</span></span>  
  
|<span data-ttu-id="72563-628">Atrybut</span><span class="sxs-lookup"><span data-stu-id="72563-628">Attribute</span></span>|<span data-ttu-id="72563-629">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-629">Description</span></span>|<span data-ttu-id="72563-630">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-630">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="72563-631">name</span><span class="sxs-lookup"><span data-stu-id="72563-631">name</span></span>|<span data-ttu-id="72563-632">Nazwa zmiennej.</span><span class="sxs-lookup"><span data-stu-id="72563-632">The name of the variable.</span></span>|<span data-ttu-id="72563-633">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-633">Yes</span></span>|  
|<span data-ttu-id="72563-634">wartość</span><span class="sxs-lookup"><span data-stu-id="72563-634">value</span></span>|<span data-ttu-id="72563-635">Wartość zmiennej.</span><span class="sxs-lookup"><span data-stu-id="72563-635">The value of the variable.</span></span> <span data-ttu-id="72563-636">Może to być wyrażenie lub ciągiem literałowym.</span><span class="sxs-lookup"><span data-stu-id="72563-636">This can be an expression or a literal value.</span></span>|<span data-ttu-id="72563-637">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-637">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="72563-638">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="72563-638">Usage</span></span>  
 <span data-ttu-id="72563-639">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72563-639">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72563-640">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="72563-640">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="72563-641">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="72563-641">**Policy scopes:** all scopes</span></span>  
  
###  <span data-ttu-id="72563-642"><a name="set-variableAllowedTypes"></a>Dozwolonymi typami</span><span class="sxs-lookup"><span data-stu-id="72563-642"><a name="set-variableAllowedTypes"></a> Allowed types</span></span>  
 <span data-ttu-id="72563-643">Wyrażenia używane w `set-variable` zasad musi zwracać jedną z następujących typów podstawowych.</span><span class="sxs-lookup"><span data-stu-id="72563-643">Expressions used in the `set-variable` policy must return one of the following basic types.</span></span>  
  
-   <span data-ttu-id="72563-644">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="72563-644">System.Boolean</span></span>  
  
-   <span data-ttu-id="72563-645">System.SByte</span><span class="sxs-lookup"><span data-stu-id="72563-645">System.SByte</span></span>  
  
-   <span data-ttu-id="72563-646">System.Byte</span><span class="sxs-lookup"><span data-stu-id="72563-646">System.Byte</span></span>  
  
-   <span data-ttu-id="72563-647">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="72563-647">System.UInt16</span></span>  
  
-   <span data-ttu-id="72563-648">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="72563-648">System.UInt32</span></span>  
  
-   <span data-ttu-id="72563-649">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="72563-649">System.UInt64</span></span>  
  
-   <span data-ttu-id="72563-650">System.Int16</span><span class="sxs-lookup"><span data-stu-id="72563-650">System.Int16</span></span>  
  
-   <span data-ttu-id="72563-651">System.Int32</span><span class="sxs-lookup"><span data-stu-id="72563-651">System.Int32</span></span>  
  
-   <span data-ttu-id="72563-652">System.Int64</span><span class="sxs-lookup"><span data-stu-id="72563-652">System.Int64</span></span>  
  
-   <span data-ttu-id="72563-653">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="72563-653">System.Decimal</span></span>  
  
-   <span data-ttu-id="72563-654">System.Single</span><span class="sxs-lookup"><span data-stu-id="72563-654">System.Single</span></span>  
  
-   <span data-ttu-id="72563-655">System.Double</span><span class="sxs-lookup"><span data-stu-id="72563-655">System.Double</span></span>  
  
-   <span data-ttu-id="72563-656">System.Guid</span><span class="sxs-lookup"><span data-stu-id="72563-656">System.Guid</span></span>  
  
-   <span data-ttu-id="72563-657">System.String</span><span class="sxs-lookup"><span data-stu-id="72563-657">System.String</span></span>  
  
-   <span data-ttu-id="72563-658">System.Char</span><span class="sxs-lookup"><span data-stu-id="72563-658">System.Char</span></span>  
  
-   <span data-ttu-id="72563-659">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="72563-659">System.DateTime</span></span>  
  
-   <span data-ttu-id="72563-660">Obiekt System.TimeSpan</span><span class="sxs-lookup"><span data-stu-id="72563-660">System.TimeSpan</span></span>  
  
-   <span data-ttu-id="72563-661">System.Byte?</span><span class="sxs-lookup"><span data-stu-id="72563-661">System.Byte?</span></span>  
  
-   <span data-ttu-id="72563-662">System.UInt16?</span><span class="sxs-lookup"><span data-stu-id="72563-662">System.UInt16?</span></span>  
  
-   <span data-ttu-id="72563-663">System.UInt32?</span><span class="sxs-lookup"><span data-stu-id="72563-663">System.UInt32?</span></span>  
  
-   <span data-ttu-id="72563-664">System.UInt64?</span><span class="sxs-lookup"><span data-stu-id="72563-664">System.UInt64?</span></span>  
  
-   <span data-ttu-id="72563-665">System.Int16?</span><span class="sxs-lookup"><span data-stu-id="72563-665">System.Int16?</span></span>  
  
-   <span data-ttu-id="72563-666">System.Int32?</span><span class="sxs-lookup"><span data-stu-id="72563-666">System.Int32?</span></span>  
  
-   <span data-ttu-id="72563-667">System.Int64?</span><span class="sxs-lookup"><span data-stu-id="72563-667">System.Int64?</span></span>  
  
-   <span data-ttu-id="72563-668">System.Decimal?</span><span class="sxs-lookup"><span data-stu-id="72563-668">System.Decimal?</span></span>  
  
-   <span data-ttu-id="72563-669">System.Single?</span><span class="sxs-lookup"><span data-stu-id="72563-669">System.Single?</span></span>  
  
-   <span data-ttu-id="72563-670">System.Double?</span><span class="sxs-lookup"><span data-stu-id="72563-670">System.Double?</span></span>  
  
-   <span data-ttu-id="72563-671">System.Guid?</span><span class="sxs-lookup"><span data-stu-id="72563-671">System.Guid?</span></span>  
  
-   <span data-ttu-id="72563-672">System.String?</span><span class="sxs-lookup"><span data-stu-id="72563-672">System.String?</span></span>  
  
-   <span data-ttu-id="72563-673">System.Char?</span><span class="sxs-lookup"><span data-stu-id="72563-673">System.Char?</span></span>  
  
-   <span data-ttu-id="72563-674">System.DateTime?</span><span class="sxs-lookup"><span data-stu-id="72563-674">System.DateTime?</span></span>  

##  <span data-ttu-id="72563-675"><a name="Trace"></a>Śledzenia</span><span class="sxs-lookup"><span data-stu-id="72563-675"><a name="Trace"></a> Trace</span></span>  
 <span data-ttu-id="72563-676">`trace` Zasad dodaje ciąg do [inspektora interfejsu API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="72563-676">The             `trace` policy adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span> <span data-ttu-id="72563-677">Zasady będą wykonywane tylko gdy śledzenie jest wyzwalane, tj. `Ocp-Apim-Trace` nagłówek żądania jest obecny i ustaw do `true` i `Ocp-Apim-Subscription-Key` nagłówek żądania jest obecny i ma prawidłowy klucz, skojarzone z kontem administratora.</span><span class="sxs-lookup"><span data-stu-id="72563-677">The policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set to `true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with the admin account.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="72563-678">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="72563-678">Policy statement</span></span>  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="72563-679">Elementy</span><span class="sxs-lookup"><span data-stu-id="72563-679">Elements</span></span>  
  
|<span data-ttu-id="72563-680">Element</span><span class="sxs-lookup"><span data-stu-id="72563-680">Element</span></span>|<span data-ttu-id="72563-681">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-681">Description</span></span>|<span data-ttu-id="72563-682">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-682">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="72563-683">śledzenia</span><span class="sxs-lookup"><span data-stu-id="72563-683">trace</span></span>|<span data-ttu-id="72563-684">Element główny.</span><span class="sxs-lookup"><span data-stu-id="72563-684">Root element.</span></span>|<span data-ttu-id="72563-685">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-685">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72563-686">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="72563-686">Attributes</span></span>  
  
|<span data-ttu-id="72563-687">Atrybut</span><span class="sxs-lookup"><span data-stu-id="72563-687">Attribute</span></span>|<span data-ttu-id="72563-688">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-688">Description</span></span>|<span data-ttu-id="72563-689">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-689">Required</span></span>|<span data-ttu-id="72563-690">Domyślne</span><span class="sxs-lookup"><span data-stu-id="72563-690">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="72563-691">Źródło</span><span class="sxs-lookup"><span data-stu-id="72563-691">source</span></span>|<span data-ttu-id="72563-692">Literał ciągu zrozumiały dla przeglądarki śledzenia i Określanie źródła komunikatu.</span><span class="sxs-lookup"><span data-stu-id="72563-692">String literal meaningful to the trace viewer and specifying the source of the message.</span></span>|<span data-ttu-id="72563-693">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-693">Yes</span></span>|<span data-ttu-id="72563-694">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="72563-694">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="72563-695">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="72563-695">Usage</span></span>  
 <span data-ttu-id="72563-696">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="72563-696">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="72563-697">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="72563-697">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="72563-698">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="72563-698">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="72563-699"><a name="Wait"></a>Oczekiwania</span><span class="sxs-lookup"><span data-stu-id="72563-699"><a name="Wait"></a> Wait</span></span>  
 <span data-ttu-id="72563-700">`wait` Zasad wykonuje jego zasadami bezpośrednio podrzędne równolegle i czeka na wszystkich lub jednego z jego zasadami bezpośrednio podrzędne, aby ukończyć przed zakończeniem działania.</span><span class="sxs-lookup"><span data-stu-id="72563-700">The `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies to complete before it completes.</span></span> <span data-ttu-id="72563-701">Zasady oczekiwania może mieć jako jego zasadami bezpośrednio podrzędne [żądanie wysłania](api-management-advanced-policies.md#SendRequest), [pobrać wartości z pamięci podręcznej](api-management-caching-policies.md#GetFromCacheByKey), i [sterowania przepływem](api-management-advanced-policies.md#choose) zasad.</span><span class="sxs-lookup"><span data-stu-id="72563-701">The wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="72563-702">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="72563-702">Policy statement</span></span>  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a><span data-ttu-id="72563-703">Przykład</span><span class="sxs-lookup"><span data-stu-id="72563-703">Example</span></span>  
 <span data-ttu-id="72563-704">W poniższym przykładzie występują dwa `choose` zasad jako zasady bezpośrednio podrzędne `wait` zasad.</span><span class="sxs-lookup"><span data-stu-id="72563-704">In the following example there are two `choose` policies as immediate child policies of the `wait` policy.</span></span> <span data-ttu-id="72563-705">Każdy z tych `choose` zasad wykonywane równolegle.</span><span class="sxs-lookup"><span data-stu-id="72563-705">Each of these `choose` policies executes in parallel.</span></span> <span data-ttu-id="72563-706">Każdy `choose` zasad próbuje pobrać wartość w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="72563-706">Each `choose` policy attempts to retrieve a cached value.</span></span> <span data-ttu-id="72563-707">W przypadku Chybienie pamięci podręcznej usługi wewnętrznej bazy danych jest wywoływana podania wartości.</span><span class="sxs-lookup"><span data-stu-id="72563-707">If there is a cache miss, a backend service is called to provide the value.</span></span> <span data-ttu-id="72563-708">W tym przykładzie `wait` zasad nie zostanie zakończone do czasu ukończenia wszystkich swoich zasad bezpośrednio podrzędne, ponieważ `for` atrybut ma ustawioną `all`.</span><span class="sxs-lookup"><span data-stu-id="72563-708">In this example the `wait` policy does not complete until all of its immediate child policies complete, because the `for` attribute is set to `all`.</span></span>   <span data-ttu-id="72563-709">W tym przykładzie zmienne kontekstu (`execute-branch-one`, `value-one`, `execute-branch-two`, i `value-two`) są deklarowane jako poza zakres tego przykład zasad.</span><span class="sxs-lookup"><span data-stu-id="72563-709">In this example the context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of the scope of this example policy.</span></span>  
  
```xml  
<wait for="all">  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-one="])">  
      <cache-lookup-value key="key-one" variable-name="value-one" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-one="))">  
          <send-request mode="new" response-variable-name="value-one">  
            <set-url>https://backend-one</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-two="])">  
      <cache-lookup-value key="key-two" variable-name="value-two" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-two="))">  
          <send-request mode="new" response-variable-name="value-two">  
            <set-url>https://backend-two</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
</wait>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="72563-710">Elementy</span><span class="sxs-lookup"><span data-stu-id="72563-710">Elements</span></span>  
  
|<span data-ttu-id="72563-711">Element</span><span class="sxs-lookup"><span data-stu-id="72563-711">Element</span></span>|<span data-ttu-id="72563-712">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-712">Description</span></span>|<span data-ttu-id="72563-713">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-713">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="72563-714">oczekiwania</span><span class="sxs-lookup"><span data-stu-id="72563-714">wait</span></span>|<span data-ttu-id="72563-715">Element główny.</span><span class="sxs-lookup"><span data-stu-id="72563-715">Root element.</span></span> <span data-ttu-id="72563-716">Może zawierać jako elementy podrzędne tylko `send-request`, `cache-lookup-value`, i `choose` zasad.</span><span class="sxs-lookup"><span data-stu-id="72563-716">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span></span>|<span data-ttu-id="72563-717">Tak</span><span class="sxs-lookup"><span data-stu-id="72563-717">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="72563-718">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="72563-718">Attributes</span></span>  
  
|<span data-ttu-id="72563-719">Atrybut</span><span class="sxs-lookup"><span data-stu-id="72563-719">Attribute</span></span>|<span data-ttu-id="72563-720">Opis</span><span class="sxs-lookup"><span data-stu-id="72563-720">Description</span></span>|<span data-ttu-id="72563-721">Wymagane</span><span class="sxs-lookup"><span data-stu-id="72563-721">Required</span></span>|<span data-ttu-id="72563-722">Domyślne</span><span class="sxs-lookup"><span data-stu-id="72563-722">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="72563-723">dla</span><span class="sxs-lookup"><span data-stu-id="72563-723">for</span></span>|<span data-ttu-id="72563-724">Określa, czy `wait` czeka zasady dla wszystkich zasad bezpośrednio podrzędne być wykonane lub tylko jeden.</span><span class="sxs-lookup"><span data-stu-id="72563-724">Determines whether the `wait` policy waits for all immediate child policies to be completed or just one.</span></span> <span data-ttu-id="72563-725">Dozwolone wartości to:</span><span class="sxs-lookup"><span data-stu-id="72563-725">Allowed values are:</span></span><br /><br /> <span data-ttu-id="72563-726">-   `all`-Poczekaj, aż wszystkie zasady bezpośrednio podrzędne do ukończenia</span><span class="sxs-lookup"><span data-stu-id="72563-726">-   `all` - wait for all immediate child policies to complete</span></span><br /><span data-ttu-id="72563-727">-wszelkie - poczekaj dowolne zasady bezpośrednio podrzędne zakończyć.</span><span class="sxs-lookup"><span data-stu-id="72563-727">-   any - wait for any immediate child policy to complete.</span></span> <span data-ttu-id="72563-728">Po zakończeniu pierwszego zasad bezpośrednio podrzędne `wait` kończy zasad i wykonywania innych zasad bezpośrednio podrzędne zostanie zakończony.</span><span class="sxs-lookup"><span data-stu-id="72563-728">Once the first immediate child policy has completed, the `wait` policy completes and execution of any other immediate child policies is terminated.</span></span>|<span data-ttu-id="72563-729">Nie</span><span class="sxs-lookup"><span data-stu-id="72563-729">No</span></span>|<span data-ttu-id="72563-730">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="72563-730">all</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="72563-731">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="72563-731">Usage</span></span>  
 <span data-ttu-id="72563-732">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="72563-732">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="72563-733">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="72563-733">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="72563-734">**Zakresy zasad:**wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="72563-734">**Policy scopes:**all scopes</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="72563-735">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="72563-735">Next steps</span></span>
<span data-ttu-id="72563-736">Aby uzyskać więcej informacji, Praca z zasad Zobacz:</span><span class="sxs-lookup"><span data-stu-id="72563-736">For more information working with policies, see:</span></span>
-   [<span data-ttu-id="72563-737">Zasady w usłudze API Management</span><span class="sxs-lookup"><span data-stu-id="72563-737">Policies in API Management</span></span>](api-management-howto-policies.md) 
-   [<span data-ttu-id="72563-738">Wyrażenia zasad</span><span class="sxs-lookup"><span data-stu-id="72563-738">Policy expressions</span></span>](api-management-policy-expressions.md)
